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

This overview maps to specific implementation steps below:

### Phase 1: Domain Understanding (→ Steps 1, 2, 2b)
1. **Engage with user** to clarify requirements (Step 1)
2. **Analyze existing examples** in `.claude/docs/` as references (Step 2)
3. **Research domain** if needed via domain-researcher agent (Step 2b)

### Phase 2: Toolkit Generation (→ Steps 3-8)
Based on research and user requirements:
1. **Directory structure** appropriate for the domain (Step 3)
2. **Sub-agents** specialized for domain tasks (Step 4)
3. **Custom commands** for common workflows (Step 5)
4. **Configuration files** with correct formats (Step 6)
5. **Optional scripts** if domain requires (Step 7)
6. **Scaffolding command** for reusability (Step 8)

### Phase 3: Finalization (→ Steps 9-10)
1. **Documentation** with guidelines (Step 9)
2. **Validation** and testing instructions (Step 10)

## Implementation Instructions

When executed, follow these steps:

### Step 1: User Engagement and Clarification

Engage with the user to understand their specific needs based on `$domain_description`:

**Generate clarifying questions relative to their input:**
```
User: "$domain_description"
Claude: "I'll help create a toolkit for $domain_description. To make it perfect for your needs:
[Generate 3-5 relevant questions based on their specific domain]
```

**Check for custom resources:**
- If user mentions a folder path → read and analyze it
- If user references `.md` files → incorporate as requirements
- If user has existing project structure → use as template

**Example interactions:**
- Input: "React Native toolkit"
  → Ask about: iOS/Android focus, Expo vs bare, state management, UI libraries
- Input: "Python data science toolkit"
  → Ask about: Jupyter/scripts, ML frameworks, visualization needs, deployment targets
- Input: "using template in /my-template"
  → Read the template structure and ask about modifications needed

### Step 2: Domain Assessment and Example Analysis

1. **List ALL files in `.claude/docs/`** - these serve as reference examples for quality
2. **Read existing toolkit reports** to understand expected structure:
   - `Branch_Co-authoring_AI_prompt.md` - comprehensive example (~300 lines)
   - `nextjs_toolkit_report_example.md` - detailed web patterns (~900 lines)
   - Any other `.md` files = potential user examples or custom requirements
3. **Analyze user's custom resources** (if provided):
   - Read folder structures they reference
   - Incorporate boilerplate code patterns
   - Extract conventions and preferences
4. **Determine approach**:
   - These are EXAMPLES of quality, not rigid templates
   - Each toolkit should be tailored to the specific domain
   - If new domain → proceed to Step 2b for research

### Step 2b: Launching Domain Researcher

When domain research is needed, launch with full context:
```
@domain-researcher Create comprehensive toolkit report for: "$domain_description"

Context from user engagement:
- [Include all clarification answers from Step 1]
- [Reference any custom templates: $paths]

Quality requirements:
- Match depth of example reports (~500-900 lines of substantive content)
- Include 15+ authoritative references
- Provide code examples and implementation details
- Research current best practices (2024-2025)
```

When domain-researcher completes:
1. Read the generated report from `.claude/docs/`
2. Extract key sections (agents, commands, structure)
3. Use as blueprint for remaining generation steps

### Step 3: Directory Creation

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

### Step 4: Agent Generation

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

### Step 5: Command Creation

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

### Step 6: Configuration Files

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
  }
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

### Step 7: Domain-Specific Scripts (Optional)

Only create shell scripts if the domain specifically requires them:

**Examples:**
- Web projects might need deployment scripts
- Data science might need data processing scripts
- Mobile apps might need build scripts

**Note:** The scaffolding command (Step 7) is a Claude command, not a shell script

### Step 8: Scaffolding Command

Create a setup command for the generated toolkit (e.g., `/setup-[domain]`):
- Allows users to create multiple projects from the template
- Copies the entire structure to a new directory
- Updates project-specific configurations
- Initializes git repository
- Similar to how `.claude/commands/setup-coauthor-example` works for book projects

Example: `/setup-nextjs my-landing-page` creates a new instance from the Next.js toolkit template

### Step 9: Documentation

Generate PROJECT.md with:
1. Domain-specific mission statement
2. Coding standards and conventions
3. Workflow guidelines
4. Command reference
5. **CRITICAL**: Instructions to start Claude Code from project directory

### Step 10: Validation
1. **Verify JSON files** are valid (settings.json, project.json if created)
2. **Check command files** exist in `.claude/commands/`
3. **Ensure PROJECT.md** was created with guidelines
4. **Note for user**: Test the scaffolding command by:
   - Exit Claude Code
   - Navigate to generated project: `cd [project-name]`
   - Start Claude from within: `claude`
   - Try the scaffolding command: `/setup-[domain] test-project`

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