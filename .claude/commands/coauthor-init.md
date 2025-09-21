---
name: coauthor-init
description: Meta-framework generator for creating domain-specific AI co-authoring toolkits
arguments:
  domain_description:
    description: Description of the toolkit you want to create (e.g., "Nextjs landing page builder", "mobile app developer", "research paper writer")
    type: string
    required: true
  project_name:
    description: Name for the generated project directory (defaults to domain-toolkit)
    type: string
    required: false
---

# Co-Author Init - Meta-Framework Generator

## Purpose

This command creates complete AI-assisted development toolkits for any domain by:
1. Analyzing your domain requirements
2. Researching best practices (if needed)
3. Generating appropriate agents, commands, and workflows
4. Setting up the entire project structure with proper configurations

## Process Flow

### Phase 1: Domain Analysis
1. **Parse user input** to understand the domain (web, mobile, data science, writing, etc.)
2. **Check `.claude/docs/` for existing domain reports**
3. **If no report exists**, launch domain-researcher agent to create one
4. **Load or generate** the domain-specific toolkit report

### Phase 2: Toolkit Generation
Based on the report, create:
1. **Directory structure** appropriate for the domain
2. **Sub-agents** specialized for domain tasks
3. **Custom commands** for common workflows
4. **Output styles** for communication modes
5. **Automation scripts** for batch operations
6. **Configuration files** with correct formats

### Phase 3: Project Setup
1. Initialize git repository
2. Create README with quickstart guide
3. Set up example workflows
4. Configure default permissions
5. Add domain-specific templates

## Implementation Instructions

When executed, follow these steps:

### Step 1: Domain Assessment
```python
# Pseudo-logic for domain detection
if "book" or "manuscript" or "writing" in domain_description:
    report = ".claude/docs/Branch_Co-authoring_AI_prompt.md"
elif exists(f".claude/docs/{domain}_toolkit_report.md"):
    report = f".claude/docs/{domain}_toolkit_report.md"
else:
    # Launch domain researcher
    report = research_domain(domain_description)
```

### Step 2: Directory Creation

Create structure based on domain. Examples:

**For Web Development:**
```
project-name/
├── src/               # Source code
├── public/            # Static assets
├── components/        # Reusable components
├── tests/             # Test files
├── docs/              # Documentation
├── .claude/
│   ├── commands/
│   ├── agents/
│   ├── output-styles/
│   └── settings.json
└── PROJECT.md
```

**For Mobile Apps:**
```
project-name/
├── app/               # Application code
├── screens/           # Screen components
├── services/          # API and data services
├── assets/            # Images, fonts
├── tests/
├── .claude/
└── PROJECT.md
```

### Step 3: Agent Generation

Create agents based on domain needs:

**Web Development Agents:**
- `component-builder` - Creates React/Vue/Angular components
- `style-designer` - Manages CSS and design systems
- `api-connector` - Integrates with backends
- `test-writer` - Generates test suites
- `deployer` - Handles deployment workflows

**Data Science Agents:**
- `data-explorer` - Analyzes datasets
- `model-trainer` - Builds ML models
- `visualizer` - Creates charts and plots
- `report-generator` - Documents findings

### Step 4: Command Creation

Generate domain-specific commands:

**Web Development:**
- `/create-component <name>` - Scaffolds new component
- `/style-theme` - Generates consistent theme
- `/optimize-performance` - Analyzes and improves speed
- `/deploy-preview` - Creates staging deployment

**Mobile Development:**
- `/create-screen <name>` - New screen with navigation
- `/generate-api` - Creates API service layer
- `/test-device <platform>` - Platform-specific testing

### Step 5: Configuration Files

#### settings.json (MUST use correct format):
```json
{
  "permissions": {
    "allow": [
      "Read(src/**)",
      "Write(src/**)",
      "Edit(src/**)",
      "MultiEdit(src/**)"
    ],
    "ask": [
      "Bash(npm:*)",
      "Bash(git:*)",
      "WebSearch"
    ],
    "deny": [
      "Read(.env)",
      "Bash(rm -rf:*)",
      "Bash(sudo:*)"
    ]
  },
  "outputStyle": "default"
}
```

#### project.json (for metadata):
```json
{
  "name": "project-name",
  "domain": "web-development",
  "framework": "nextjs",
  "version": "1.0.0",
  "agents": {
    "available": ["component-builder", "style-designer", ...]
  }
}
```

### Step 6: Shell Scripts

Create domain-appropriate automation:

**For Web:**
- `build.sh` - Build production bundle
- `test-all.sh` - Run complete test suite
- `deploy.sh` - Deploy to production
- `component-generator.sh` - Batch component creation
- **`setup_[domain].sh`** - Scaffold script to create multiple projects from this template

### Step 7: Scaffolding Command

Create a setup command for the generated toolkit (e.g., `/setup-[domain]`):
- Allows users to create multiple projects from the template
- Copies the entire structure to a new directory
- Updates project-specific configurations
- Initializes git repository
- Similar to how `/setup-coauthor` works for book projects

Example: `/setup-nextjs my-landing-page` creates a new instance from the Next.js toolkit template

### Step 8: Documentation

Generate PROJECT.md with:
1. Domain-specific mission statement
2. Coding standards and conventions
3. Workflow guidelines
4. Command reference
5. **CRITICAL**: Instructions to start Claude Code from project directory

## Domain Examples

### Example 1: Nextjs Landing Page Toolkit
```bash
/coauthor-init "Nextjs landing page builder with Tailwind CSS" nextjs-toolkit
```
Creates:
- Component generators
- Tailwind theme manager
- SEO optimizer agent
- Deployment scripts for Vercel

### Example 2: Python Data Science Toolkit
```bash
/coauthor-init "Python data science notebook assistant" ds-toolkit
```
Creates:
- Jupyter notebook manager
- Data cleaning agents
- Visualization generators
- Model comparison tools

### Example 3: Mobile App Toolkit
```bash
/coauthor-init "React Native mobile app developer" mobile-toolkit
```
Creates:
- Screen generators
- State management setup
- Platform-specific handlers
- App store deployment scripts

## Error Handling

1. **Missing domain report**: Automatically launch domain-researcher
2. **Invalid settings.json**: Use settings-simple.json template
3. **Permission errors**: Default to restrictive permissions
4. **Missing tools**: Suggest installation commands

## Success Criteria

The generated toolkit should:
1. Be immediately usable for the specified domain
2. Include all necessary agents and commands
3. Have valid configuration files
4. Provide clear documentation
5. Follow proven patterns from our book toolkit
6. **Emphasize**: User must start Claude Code from project directory

## Output Message

After successful generation:
```
✅ [Domain] Toolkit Successfully Created!

📂 Project: [project-name]/
📚 Domain: [domain]
🤖 Agents: [count] specialized agents
⚡ Commands: [count] custom commands
🔧 Scripts: [count] automation scripts

IMPORTANT: To use this toolkit:
1. cd [project-name]
2. claude  # Start Claude Code FROM WITHIN the project
3. /help   # See available commands

Next steps:
- Review PROJECT.md for guidelines
- Try example commands
- Customize agents as needed
```

## Notes

- This command replaces the need for domain-specific setup commands
- Leverages proven patterns from book co-authoring toolkit
- Ensures consistent structure across all domain toolkits
- Incorporates all fixes for settings.json and naming conventions
- Can be extended with new domains as reports are created