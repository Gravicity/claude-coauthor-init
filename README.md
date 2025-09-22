# Claude Co-Author Init - Meta-Framework Generator

A universal AI toolkit generator that creates specialized Claude Code co-authoring environments for any domain - from web development to data science, mobile apps to technical writing.

## 🚀 What is This?

This is a **meta-framework generator** - it creates complete AI-assisted development toolkits tailored to your specific needs. Instead of building one-size-fits-all solutions, it researches your domain and generates:

- 🤖 **Specialized AI agents** for your workflow
- ⚡ **Custom commands** for common tasks
- 📁 **Proper project structure** for your domain
- 🔧 **Automation scripts** specific to your tools
- 📚 **Documentation** tailored to your needs

## 🎯 Key Features

### Intelligent Domain Research
- Automatically researches unfamiliar domains
- Adapts proven patterns to new contexts
- Generates comprehensive toolkit reports

### Complete Toolkit Generation
- Creates all necessary agents and commands
- Sets up proper file structures
- Configures permissions correctly
- Includes automation scripts
- **Generates scaffolding command** to create multiple projects from your toolkit

### Universal Application
Works for any domain:
- **Web Development**: React, Vue, Next.js, etc.
- **Mobile Apps**: React Native, Flutter, Swift
- **Data Science**: Python notebooks, R, Julia
- **Backend APIs**: Node.js, Python, Go, Rust
- **Documentation**: Technical writing, blogs, tutorials
- **And more**: Game development, IoT, DevOps, etc.

## 📦 Installation

1. **Clone this repository:**
   ```bash
   git clone https://github.com/Gravicity/claude-coauthor-init.git
   cd claude-coauthor-init
   ```

2. **Start Claude Code from this directory:**
   ```bash
   claude
   ```

   ⚠️ **IMPORTANT**: You must start Claude Code from within the `claude-coauthor-init` directory for the commands to work!

## 🔨 Usage

### Basic Usage

Generate a toolkit for your domain:

```bash
/coauthor-init "Next.js landing page builder" my-landing-toolkit
```

**Claude will engage with you**, asking clarifying questions specific to your domain to ensure the toolkit perfectly matches your needs.

### Examples

**Web Development Toolkit:**
```bash
/coauthor-init "React component library with Storybook" component-toolkit
```
→ Claude asks: Component style? Testing approach? Documentation format?

**Data Science Toolkit:**
```bash
/coauthor-init "Python data analysis with Jupyter notebooks" data-toolkit
```
→ Claude asks: ML frameworks? Visualization tools? Deployment targets?

**Mobile App Toolkit:**
```bash
/coauthor-init "React Native app with Expo" mobile-toolkit
```
→ Claude asks: iOS/Android/both? State management? UI library preferences?

**Using Your Own Templates:**
```bash
/coauthor-init "API toolkit using my template in /api-boilerplate" custom-api-toolkit
```
→ Claude analyzes your template and asks about modifications needed

**Reference Existing Documentation:**
```bash
/coauthor-init "Toolkit following patterns in docs/architecture.md" architecture-toolkit
```
→ Claude reads your documentation and incorporates your patterns

### After Generation

Once your toolkit is created:

1. **Navigate to your new project:**
   ```bash
   cd my-toolkit
   ```

2. **Start Claude Code from within the project:**
   ```bash
   claude
   ```

   ⚠️ **IMPORTANT**: You must start Claude Code from inside your project directory for the custom settings to work!

3. **Use your domain-specific commands:**
   - View available commands with `/help`
   - Check agents with `@help`
   - Read PROJECT.md for guidelines
   - Use the generated setup command (e.g., `/setup-nextjs`) to scaffold new projects

## 📂 What Gets Generated

Each toolkit includes:

```
your-toolkit/
├── src/ (or appropriate source directory)
├── tests/
├── docs/
├── .claude/
│   ├── commands/        # Domain-specific commands
│   ├── agents/          # Specialized AI agents
│   ├── output-styles/   # Communication modes
│   └── settings.json    # Proper permissions
├── bin/                 # Automation scripts & setup command
├── PROJECT.md           # Project guidelines
└── README.md            # Getting started guide

**Plus a scaffolding command** like `/setup-nextjs` that lets you create multiple projects from this toolkit template!
```

## 🤖 How It Works

### The Intelligent Generation Process

1. **🗣️ User Engagement**: Claude asks clarifying questions tailored to your specific domain
2. **🔍 Smart Detection**: Automatically finds and analyzes:
   - Your custom templates (if you reference folders)
   - Your documentation (if you mention .md files)
   - Existing examples for quality benchmarks
3. **📚 Deep Research**: When needed, performs multiple rounds of research:
   - Official documentation and best practices
   - Community patterns and tools
   - Testing and deployment strategies
   - Performance optimization techniques
4. **🏗️ Toolkit Generation**: Creates your complete toolkit:
   - Domain-specific agents (6-10 specialized assistants)
   - Custom commands (8-12 workflow accelerators)
   - Proper project structure
   - Configuration with correct permissions
5. **♻️ Reusability**: Generates a scaffolding command so you can create multiple projects from your toolkit
6. **✅ Validation**: Provides testing instructions to ensure everything works

## 📚 Reference Examples & Quality Standards

The system learns from high-quality examples to ensure consistency:

### Example Reports
In `.claude/docs/` you'll find reference examples:
- **Branch Co-authoring** (~300 lines): Book/manuscript toolkit example
- **Next.js Toolkit** (~900 lines): Comprehensive web development example

### What Gets Researched
For new domains, the system performs deep research to create reports with:
- **500-900 lines** of substantive, detailed content
- **15+ authoritative references** with current best practices (2024-2025)
- **Practical code examples** throughout
- **6-10 specialized agents** with clear capabilities
- **8-12 custom commands** with implementation details
- **Complete sections** without placeholders or TODOs

### Custom Templates
You can provide your own:
- **Existing projects**: Reference a folder with your boilerplate
- **Documentation**: Point to .md files with your patterns
- **Examples**: Add more reference reports to `.claude/docs/`

## ⚙️ Configuration

### Settings Format

Uses validated settings.json format:
```json
{
  "permissions": {
    "allow": ["Read(src/**)", "Write(src/**)", ...],
    "ask": ["Bash(npm:*)", "WebSearch"],
    "deny": ["Read(.env)", "Bash(sudo:*)"]
  }
}
```

### Project Metadata

Stores metadata in project.json:
```json
{
  "name": "your-toolkit",
  "domain": "web-development",
  "framework": "nextjs",
  "agents": {...}
}
```

## 🔄 Reusing Your Toolkit

Each generated toolkit includes its own scaffolding command! After creating a toolkit, you can use it as a template:

```bash
# Example: If you generated a Next.js toolkit
cd nextjs-toolkit
claude

# Now create multiple projects from this template:
/setup-nextjs my-first-landing
/setup-nextjs my-second-app
/setup-nextjs client-project
```

Each scaffolded project gets:
- All the agents and commands from your toolkit
- Proper directory structure
- Configured settings
- Your customizations and patterns

## 🎯 Key Features That Make This Special

### Intelligent Conversation
Unlike rigid generators, this system **engages with you** to understand exactly what you need. It asks smart questions based on your specific domain.

### Learn From Your Work
If you have existing templates, boilerplate code, or documentation, just reference them! The system will:
- Read and analyze your existing patterns
- Incorporate your conventions and preferences
- Build on what you've already created

### Research-Driven Quality
For unfamiliar domains, the system doesn't guess - it **researches**:
- Multiple rounds of targeted searches
- Current best practices (2024-2025)
- Real-world patterns from production codebases
- Community-validated approaches

### Comprehensive Output
Every toolkit includes:
- Detailed PROJECT.md with your coding standards
- Specialized AI agents that understand your domain
- Custom commands for your specific workflows
- Proper configuration with security in mind
- Optional automation hooks for advanced users

## 🛠️ Customization

After generation, you can:
- Edit agents in `.claude/agents/`
- Add commands in `.claude/commands/`
- Modify output styles in `.claude/output-styles/`
- Adjust permissions in `settings.json`
- Update guidelines in PROJECT.md

## 🐛 Troubleshooting

### "Invalid Settings" Error
- The generator uses validated settings.json formats
- Only includes supported fields (permissions only)
- Hooks are configured separately, not in settings.json

### Commands Not Working
- Ensure you started Claude Code from the project directory
- Check that `.claude/` folder exists
- Verify command files are properly formatted

### Domain Not Recognized
- Claude will ask clarifying questions to understand better
- The system performs multiple research rounds for new domains
- You can provide examples or templates to guide generation
- Check `.claude/docs/` for the generated research report

## 🤝 Contributing

To add new domain templates:
1. Create a report in `.claude/docs/[domain]_toolkit_report.md`
2. Follow the structure of existing reports
3. Include correct JSON formats
4. Test the generation

## 📄 License

This project is open source and available for use in creating AI-assisted development environments.

## 🙏 Acknowledgments

Based on:
- Anthropic's Claude Code best practices
- Community guides by Sid Bharath and others
- The original Branch Co-authoring AI prompt report

---

## Quick Start Example

```bash
# 1. Clone the repository
git clone https://github.com/Gravicity/claude-coauthor-init.git
cd claude-coauthor-init

# 2. Start Claude Code in this directory
claude

# 3. Generate your custom toolkit (Claude will ask clarifying questions!)
/coauthor-init "Vue.js admin dashboard builder" admin-toolkit

# Claude: "I'll help create a Vue.js admin dashboard toolkit. To optimize for your needs:
#  - Will you use Vue 2 or Vue 3?
#  - Which UI framework (Vuetify, Element Plus, Ant Design Vue)?
#  - Do you need authentication/authorization?
#  - What backend will this connect to?"

# 4. Answer the questions and wait for generation

# 5. Exit Claude Code (Ctrl+C or /exit) and navigate to your new toolkit
cd admin-toolkit

# 6. Start Claude Code in your new project
claude

# 7. Start building with domain-specific AI assistance!
/create-dashboard-widget UserMetrics
@style-designer "Create a dark theme for the admin panel"
/setup-auth "Add role-based access control"
```

## 🎨 Advanced Usage

### Using Your Own Templates

```bash
# Reference an existing project structure
/coauthor-init "E-commerce platform using my template in /projects/shop-template" shop-toolkit

# Reference documentation with patterns
/coauthor-init "Microservices toolkit following docs/microservice-guide.md" microservice-toolkit

# Combine multiple references
/coauthor-init "Full-stack app using /my-backend and /my-frontend as templates" fullstack-toolkit
```

---

**Ready to revolutionize your development workflow with AI? Start generating your custom toolkit now!** 🚀