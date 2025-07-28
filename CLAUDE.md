# Instructions for Claude

This document contains important instructions and notes for Claude when working on this project.

## CRITICAL GUIDELINES

### NEVER CREATE BLOG POSTS WITHOUT CONSENT

- **NEVER CREATE BLOG POSTS WITHOUT EXPLICIT CONSENT** from mjefferson
- Do not write or propose new blog content unless specifically requested
- Only help with editing or fixing existing posts when asked

### NEVER MERGE PULL REQUESTS

- **NEVER MERGE PULL REQUESTS** - Even if explicitly asked to do so
- Only the repository owner (mjefferson) should merge PRs through the GitHub web UI
- Create PRs as requested, but do not use `gh pr merge` or similar commands
- Always provide the PR URL so that mjefferson can review and merge manually


### ALWAYS USE LATEST DEPENDENCIES

- **NEVER DOWNGRADE DEPENDENCIES** - Always use the latest stable versions
- **ALWAYS USE TOOLING TO CHECK VERSIONS** - Never guess or assume versions
- Run `pnpm outdated` to see what packages need updating
- Run `pnpm view [package] version` to check the latest published version
- When fixing dependency issues, always upgrade to the latest compatible versions
- Prioritize staying current with the ecosystem, even if it requires more work to adapt

### IMPORTANT: Development Server Limitation

- **DO NOT run `pnpm run dev`** in agent mode - this will create an endless loop and stop the agent from working properly
- Instead, use `pnpm run build` to verify your changes

## Development Process

### Testing Changes

To properly test changes, use these commands:

```bash
# Build the project (this is preferred over pnpm run dev in agent mode)
pnpm run build

# If you need to preview the build (only do when specifically requested)
pnpm run preview
```

### Project Structure

- `/src/data/blog/` - Contains all blog posts in markdown format
- `/src/pages/` - Contains page templates and routing
- `/src/components/` - Reusable UI components
- `/src/layouts/` - Page layouts and templates
- `/src/styles/` - CSS styles including Tailwind customizations

### Common Tasks

1. **Adding a new blog post**:

   - Create a new markdown file in `/src/data/blog/`
   - Include proper frontmatter (title, description, pubDatetime, etc.)
   - Format dates in ISO-8601 format: `YYYY-MM-DDTHH:MM:SS+HH:MM`
   - Format tags as arrays: `tags: ["tag1", "tag2"]`

2. **Modifying site configuration**:

   - Edit `/src/config.ts` for global site constants

3. **Styling changes**:

   - Edit files in `/src/styles/` for global styling
   - Use Tailwind classes in component templates for component-specific styling

4. **Layout changes**:

   - Modify the appropriate layout files in `/src/layouts/`

5. **Fixing broken images**:

   - Blog posts reference images in the `/public/assets/img/` directory structure
   - The original files can be found in `/temp-repos/mjeffersoncom/assets/img/`
   - Images must be copied to the matching public directory structure
   - Fixed images should be committed to the repository
   - Use `find` command to locate the original images
   - Common image paths follow the pattern: `/assets/img/YEAR/POST-NAME/IMAGE.jpg`

6. **Dependency Updates**:
   - Always use proper tooling to check for latest versions:

     ```bash
     # Check all outdated dependencies
     pnpm outdated

     # Check latest version of a specific package
     pnpm view astro version
     pnpm view react version

     # Update all dependencies to latest
     pnpm update --latest
     ```

   - Test thoroughly after updating dependencies
   - If a build fails after updates, diagnose the specific issue and FIX it properly
   - NEVER resort to downgrading as a solution

## Tech Stack

- **Astro** (latest version) - Main framework
- **TailwindCSS** - For styling
- **React** - For interactive components (v18.2.0)
- **MDX** - For enhanced markdown support