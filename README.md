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
   git clone https://github.com/yourusername/claude-coauthor-init.git
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

### Examples

**Web Development Toolkit:**
```bash
/coauthor-init "React component library with Storybook" component-toolkit
```

**Data Science Toolkit:**
```bash
/coauthor-init "Python data analysis with Jupyter notebooks" data-toolkit
```

**Mobile App Toolkit:**
```bash
/coauthor-init "React Native app with Expo" mobile-toolkit
```

**API Development Toolkit:**
```bash
/coauthor-init "Node.js REST API with Express and MongoDB" api-toolkit
```

**Documentation Toolkit:**
```bash
/coauthor-init "Technical documentation with MDX" docs-toolkit
```

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
├── bin/                 # Automation scripts
├── PROJECT.md           # Project guidelines
└── README.md            # Getting started guide
```

## 🤖 How It Works

1. **Domain Analysis**: Parses your description to understand the domain
2. **Research Phase**: Checks for existing reports or researches the domain
3. **Report Generation**: Creates a comprehensive toolkit specification
4. **Toolkit Creation**: Generates all files, agents, and commands
5. **Configuration**: Sets up proper permissions and settings
6. **Documentation**: Creates guides and examples

## 📚 Documentation Structure

The system uses domain reports to guide generation:

- **Book/Writing**: Uses the original Branch Co-authoring report
- **Next.js**: Example report for web development
- **New Domains**: Automatically researched and documented

Reports include:
- Project structure recommendations
- Agent definitions
- Command specifications
- Best practices
- Integration suggestions

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

## 🛠️ Customization

After generation, you can:
- Edit agents in `.claude/agents/`
- Add commands in `.claude/commands/`
- Modify output styles in `.claude/output-styles/`
- Adjust permissions in `settings.json`
- Update guidelines in PROJECT.md

## 🐛 Troubleshooting

### "Invalid Settings" Error
- The generator uses validated settings formats
- Check `.claude/settings.json` for syntax errors
- Use settings-simple.json if hooks cause issues

### Commands Not Working
- Ensure you started Claude Code from the project directory
- Check that `.claude/` folder exists
- Verify command files are properly formatted

### Domain Not Recognized
- The system will research unfamiliar domains
- Provide more specific descriptions if needed
- Check `.claude/docs/` for generated reports

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
git clone https://github.com/yourusername/claude-coauthor-init.git
cd claude-coauthor-init

# 2. Start Claude Code in this directory
claude

# 3. Generate your custom toolkit
/coauthor-init "Vue.js admin dashboard builder" admin-toolkit

# 4. Exit Claude Code (Ctrl+C or /exit)

# 5. Navigate to your new toolkit
cd admin-toolkit

# 6. Start Claude Code in your new project
claude

# 7. Start building with AI assistance!
/create-component UserTable
```

---

**Ready to revolutionize your development workflow with AI? Start generating your custom toolkit now!** 🚀