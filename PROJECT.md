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

## Domain Report Examples

The `.claude/docs/` folder contains reference examples that demonstrate expected quality:
- **Branch_Co-authoring_AI_prompt.md** - Comprehensive toolkit example (~300 lines)
- **nextjs_toolkit_report_example.md** - Production-grade web toolkit (~900 lines)

These serve as quality benchmarks for all generated toolkit reports:
- 500-900 lines of detailed, substantive content
- 15+ authoritative references with descriptions
- Extensive code examples and implementation details
- Complete sections without placeholders

When users provide custom examples or templates in `.claude/docs/` or reference specific folders, they're incorporated as additional requirements for the toolkit generation.

New domains are researched through multiple rounds to match this quality standard.

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