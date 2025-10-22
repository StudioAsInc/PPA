```SQL
-- =====================================================
-- Schema for AI Planning Assistant
-- =====================================================

-- 1. Create Projects Table
-- Stores the main information for each project.
CREATE TABLE IF NOT EXISTS projects (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    persona TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL
);
COMMENT ON TABLE projects IS 'Stores user projects and their configurations.';

-- 2. Create Project Files Table
-- Stores context files associated with each project.
CREATE TABLE IF NOT EXISTS project_files (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    project_id UUID NOT NULL REFERENCES projects(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    content TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL
);
COMMENT ON TABLE project_files IS 'Stores context files for each project.';


-- 3. Create Saved Prompts Table
-- Stores prompts that users have saved for a project.
CREATE TABLE IF NOT EXISTS saved_prompts (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    project_id UUID NOT NULL REFERENCES projects(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    content TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL
);
COMMENT ON TABLE saved_prompts IS 'Stores user-saved prompts for each project.';

-- =====================================================
-- 4. Enable Row Level Security (RLS)
-- =====================================================
ALTER TABLE projects ENABLE ROW LEVEL SECURITY;
ALTER TABLE project_files ENABLE ROW LEVEL SECURITY;
ALTER TABLE saved_prompts ENABLE ROW LEVEL SECURITY;

-- =====================================================
-- 5. RLS Policies
-- Ensures users can only access their own data.
-- =====================================================

-- Policies for 'projects' table
DROP POLICY IF EXISTS "Users can manage their own projects" ON projects;
CREATE POLICY "Users can manage their own projects" ON projects
    FOR ALL
    USING (auth.uid() = user_id)
    WITH CHECK (auth.uid() = user_id);

-- Policies for 'project_files' table
DROP POLICY IF EXISTS "Users can manage their own project files" ON project_files;
CREATE POLICY "Users can manage their own project files" ON project_files
    FOR ALL
    USING (auth.uid() = user_id)
    WITH CHECK (auth.uid() = user_id);

-- Policies for 'saved_prompts' table
DROP POLICY IF EXISTS "Users can manage their own saved prompts" ON saved_prompts;
CREATE POLICY "Users can manage their own saved prompts" ON saved_prompts
    FOR ALL
    USING (auth.uid() = user_id)
    WITH CHECK (auth.uid() = user_id);


-- =====================================================
-- 6. Performance Indexes
-- =====================================================
CREATE INDEX IF NOT EXISTS idx_projects_user_id ON projects(user_id);
CREATE INDEX IF NOT EXISTS idx_project_files_project_id ON project_files(project_id);
CREATE INDEX IF NOT EXISTS idx_project_files_user_id ON project_files(user_id);
CREATE INDEX IF NOT EXISTS idx_saved_prompts_project_id ON saved_prompts(project_id);
CREATE INDEX IF NOT EXISTS idx_saved_prompts_user_id ON saved_prompts(user_id);


-- =====================================================
-- 7. Functions and Triggers for `updated_at`
-- =====================================================

-- Function to update the 'updated_at' column
CREATE OR REPLACE FUNCTION handle_updated_at()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = timezone('utc'::text, now());
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger for 'projects' table
DROP TRIGGER IF EXISTS on_projects_update ON projects;
CREATE TRIGGER on_projects_update
    BEFORE UPDATE ON projects
    FOR EACH ROW
    EXECUTE FUNCTION handle_updated_at();

-- =====================================================
-- SETUP COMPLETE
-- =====================================================
```



-- WARNING: This schema is for context only and is not meant to be run.
-- Table order and constraints may not be valid for execution.

CREATE TABLE public.project_files (
  id uuid NOT NULL DEFAULT gen_random_uuid(),
  project_id uuid NOT NULL,
  user_id uuid NOT NULL,
  name text NOT NULL,
  content text,
  created_at timestamp with time zone NOT NULL DEFAULT timezone('utc'::text, now()),
  CONSTRAINT project_files_pkey PRIMARY KEY (id),
  CONSTRAINT project_files_project_id_fkey FOREIGN KEY (project_id) REFERENCES public.projects(id),
  CONSTRAINT project_files_user_id_fkey FOREIGN KEY (user_id) REFERENCES auth.users(id)
);
CREATE TABLE public.project_version_files (
  id uuid NOT NULL DEFAULT gen_random_uuid(),
  version_id uuid NOT NULL,
  name text NOT NULL,
  content text,
  CONSTRAINT project_version_files_pkey PRIMARY KEY (id),
  CONSTRAINT project_version_files_version_id_fkey FOREIGN KEY (version_id) REFERENCES public.project_versions(id)
);
CREATE TABLE public.project_versions (
  id uuid NOT NULL DEFAULT gen_random_uuid(),
  project_id uuid NOT NULL,
  user_id uuid NOT NULL,
  version_number integer NOT NULL DEFAULT nextval('project_versions_version_number_seq'::regclass),
  name text NOT NULL,
  persona text,
  model_config jsonb,
  change_summary text,
  created_at timestamp with time zone NOT NULL DEFAULT timezone('utc'::text, now()),
  CONSTRAINT project_versions_pkey PRIMARY KEY (id),
  CONSTRAINT project_versions_project_id_fkey FOREIGN KEY (project_id) REFERENCES public.projects(id),
  CONSTRAINT project_versions_user_id_fkey FOREIGN KEY (user_id) REFERENCES auth.users(id)
);
CREATE TABLE public.projects (
  id uuid NOT NULL DEFAULT gen_random_uuid(),
  user_id uuid NOT NULL,
  name text NOT NULL,
  persona text,
  created_at timestamp with time zone NOT NULL DEFAULT timezone('utc'::text, now()),
  updated_at timestamp with time zone NOT NULL DEFAULT timezone('utc'::text, now()),
  model_config jsonb,
  CONSTRAINT projects_pkey PRIMARY KEY (id),
  CONSTRAINT projects_user_id_fkey FOREIGN KEY (user_id) REFERENCES auth.users(id)
);
CREATE TABLE public.saved_prompts (
  id uuid NOT NULL DEFAULT gen_random_uuid(),
  project_id uuid NOT NULL,
  user_id uuid NOT NULL,
  name text NOT NULL,
  content text,
  created_at timestamp with time zone NOT NULL DEFAULT timezone('utc'::text, now()),
  CONSTRAINT saved_prompts_pkey PRIMARY KEY (id),
  CONSTRAINT saved_prompts_project_id_fkey FOREIGN KEY (project_id) REFERENCES public.projects(id),
  CONSTRAINT saved_prompts_user_id_fkey FOREIGN KEY (user_id) REFERENCES auth.users(id)
);