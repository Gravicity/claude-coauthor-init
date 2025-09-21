# Claude Co-Author Init - Meta-Framework Generator

## Mission
Transform Claude Code into a universal toolkit generator that creates specialized AI-assisted development environments for any domain.

## Available Commands

### `/coauthor-init <domain> [project-name]`
Generates a complete AI toolkit for your specified domain.

**Examples:**
- `/coauthor-init "Next.js landing page builder" landing-toolkit`
- `/coauthor-init "Python data science assistant" data-toolkit`
- `/coauthor-init "React Native mobile app" mobile-toolkit`

## Available Agents

### `@domain-researcher`
Researches new domains and creates comprehensive toolkit reports when no existing report is found.

## How It Works

1. **Analyze Domain**: Parse your description to understand the domain
2. **Find/Create Report**: Check for existing reports or research the domain
3. **Generate Toolkit**: Create complete project with agents, commands, and scripts
4. **Configure**: Set up proper permissions and settings
5. **Document**: Provide clear instructions and examples

## Domain Reports

Reports are stored in `.claude/docs/`:
- `Branch_Co-authoring_AI_prompt.md` - Book/manuscript writing toolkit
- `nextjs_toolkit_report_example.md` - Web development example
- New domains are researched and documented automatically

## Important Notes

⚠️ **Project Activation**: After generating a toolkit, you must:
1. Exit Claude Code
2. Navigate to the generated project directory
3. Start Claude Code from within that directory

This ensures the custom settings and commands work properly.

## File Naming Conventions

Generated toolkits follow these patterns:
- Version-based naming: `file_v1.md` → `file_v2.md`
- No status suffixes (avoid `_draft`, `_final`)
- Consistent across all agents and commands

## Settings Format

All generated projects use validated settings.json format:
- Only supported fields included
- Proper hook format with matchers
- Separate project.json for metadata

## Quick Test

Test the system with:
```
/coauthor-init "Simple test toolkit" test-project
```

Then check the generated `test-project/` directory.