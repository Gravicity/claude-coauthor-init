# **Designing the Ultimate Claude Code Co‑Authoring Toolkit**

### **Introduction**

Claude Code is Anthropic's command-line interface that wraps Claude models with agents, tools and workflows. It can read and write files, run shell commands, integrate with external services through the **Model Context Protocol (MCP)** and operate via custom **sub‑agents**. When combined with a well‑designed project structure and a **superprompt** describing the desired co‑authoring behaviour, Claude becomes a powerful partner for writing books and other long-form content. This report synthesises best practices from Anthropic's documentation, community guides and recent articles to build a production‑grade co‑authoring toolkit, expanding on each scaffolding concept from the earlier proposal.

## **1. Project Scaffold**

A good directory layout separates the manuscript, research data, scripts and configuration files. A sample structure looks like:

```
book-project/
├── manuscript/        # Draft chapters, outline and changelog
├── research/          # Notes, citations and source material
├── assets/            # Exported files (PDF, EPUB) and cover art
├── bin/               # Shell scripts for automation or headless runs
├── .claude/
│   ├── commands/      # Custom slash commands (see §6)
│   ├── agents/        # Sub‑agent definitions (see §4)
│   ├── output-styles/ # Custom output styles (see §3)
│   └── settings.json  # Permissions, hooks and project settings
└── CLAUDE.md          # Project memory and style guide (see §2)
```

Use version control (e.g. Git) and **git worktrees** to allow multiple Claude instances to work on different branches in parallel. This avoids context collisions and makes it easy to undo experiments. [1](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Git%20worktrees%20let%20you%20check,with%20Claude%20Code%2C%20this%20means)

## **2. CLAUDE.md – Project Memory**

CLAUDE.md acts as the project's memory; Claude Code reads this file at the start of every session. Anthropic's best‑practice guide recommends documenting commands, style guidelines and workflow conventions. In a co‑authoring toolkit, CLAUDE.md can include: [2](https://www.anthropic.com/engineering/claude-code-best-practices#:~:text=a.%20Create%20) [3](https://www.anthropic.com/engineering/claude-code-best-practices#:~:text=,an%20ideal%20place%20for%20documenting)

- **Mission statement and genre** – Describe the book's vision, target audience and tone.
- **Voice and style guidelines** – Outline narrative voice (e.g. cinematic, descriptive) and prose guidelines such as "concrete verbs, sensory details; minimize adverbs."
- **Structural conventions** – Describe how chapters are structured (acts, scene breaks, cliff‑hangers). Provide templates for outlines and beat sheets.
- **Research and citation notes** – Instruct Claude to flag [FACTCHECK] markers when information needs verification.
- **Working agreements** – e.g., "Prefer iterative passes: outline → scene beats → draft → revise."

Developers often refine CLAUDE.md over time and treat it as a living document. When starting a project, run `/init` to generate an initial file; edit it directly or use the `#` command to append notes during a session. [4](https://www.anthropic.com/engineering/claude-code-best-practices#:~:text=b.%20Tune%20your%20) [5](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Project%20Memory%20and%20Documentation)

## **3. Output Styles**

Output styles modify Claude's communication style without changing its core capabilities. Anthropic introduced built‑in "explanatory" and "learning" modes, which can be selected with `/output‑style explanatory` or `/output‑style learning`. **Explanatory mode** makes Claude narrate its reasoning and design choices, whereas **learning mode** encourages the user to fill in code or content while Claude acts as a mentor. [6](https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style#:~:text=Anthropic%20recently%20introduced%20new%20%E2%80%9Cexplanatory%E2%80%9D,programming%20experience) [7](https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style#:~:text=Claude%20Code%E2%80%99s%20explanatory%20mode%E2%80%A6%20explained) [8](https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style#:~:text=Explanatory%20mode%2C%20in%20many%20ways%2C,pieces%20of%20the%20implementation%20themselves)

You can create custom output styles via `/output‑style:new` and supply a description; Claude scaffolds a Markdown file which you can edit. Examples for a co‑authoring project: [9](https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style#:~:text=Creating%20a%20custom%20output%20style,for%20Claude%20Code)

- **Outline Architect** – writes high‑level outlines and beat structures, summarises arcs and themes.
- **Scene Weaver** – drafts scene‑level prose in your chosen voice.
- **Line Editor** – polishes paragraphs for tone, pacing and clarity.
- **Marketing Voice** – generates blurbs, back‑cover copy and marketing emails.

These styles complement sub‑agents: output styles shape how Claude communicates, while sub‑agents control what tasks it performs. [10](https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style#:~:text=This%20also%20highlights%20Claude%20Code%E2%80%99s,role%20of%20their%20AI%20collaborator)

## **4. Sub‑Agents**

Sub‑agents are specialised assistants with their own instructions, context windows and tool permissions. They help manage context and delegate tasks. Example sub‑agents for a writing toolkit include: [11](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Deploying%20Sub)

- **Outline Architect** – creates loglines, act structures and chapter breakdowns.
- **Researcher** – performs fact‑checking and compiles citations; uses web search via MCP servers.
- **Scene Weaver** – writes scene drafts; emphasises showing vs. telling.
- **Line Editor** – focuses on grammar, style and continuity.
- **Marketing Manager** – drafts blurbs, taglines and pitches.

To create a sub‑agent, use `/agents` and follow the prompts; Claude generates a Markdown file under `.claude/agents/`. Edit its front‑matter (name, description, allowed tools) and body instructions to specialise it. Each sub‑agent maintains its own chat history, preventing your main session from being cluttered. [12](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Setting%20up%20a%20sub,agent%20folder%20as%20markdown%20files) [13](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=,read%2C%20grep%2C%20diff%2C%20lint_runner) [14](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Each%20sub,their%20access%20to%20certain%20tools)

## **5. Custom Slash Commands**

Custom slash commands encapsulate repeatable workflows. Sid Bharath's guide notes that creating a `.claude/commands/` directory and placing Markdown files there defines new commands. Commands can call sub‑agents, run tasks and write files. Examples for a co‑authoring toolkit: [15](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Custom%20Slash%20Commands)

- **/expand-note `<note>`** – use the Outline Architect to transform a seed idea into a logline and multi‑chapter outline, and save it to `manuscript/00_outline.md`.
- **/draft-chapter `<n>`** – read the outline and have the Scene Weaver generate a chapter draft at the specified index.
- **/revise-chapter `<n>`** – send the chapter to the Line Editor for stylistic polish and continuity checks.
- **/fact-check `<n>`** – call the Researcher to verify facts in the chapter and insert [FACTCHECK] markers.
- **/marketing-pack** – ask the Marketing Manager to create a back‑cover blurb, tagline and elevator pitch from the outline and synopsis.

Custom commands are stored with the project and shared across the team. [16](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=)

## **6. Permissions and Settings**

Claude Code is conservative by default, prompting for permission before running tools or commands. You can configure permissions in `.claude/settings.json` or via `/permissions`. For writing projects, allow tools such as `Read`, `Write`, `Edit`, and restrict potentially dangerous commands.

**IMPORTANT: Settings.json Format Requirements (Claude Code 1.0+)**

The settings.json must follow strict format requirements. Many fields that seem logical are not actually supported. Here's the correct format:

```json
{
  "permissions": {
    "allow": [
      "Read(manuscript/**)",
      "Write(manuscript/**)",
      "Edit(manuscript/**)",
      "MultiEdit(manuscript/**)",
      "Read(research/**)",
      "Write(research/**)",
      "Edit(research/**)"
    ],
    "ask": [
      "Bash(pandoc:*)",
      "Bash(git commit:*)",
      "Bash(git push:*)",
      "WebSearch",
      "WebFetch"
    ],
    "deny": [
      "Read(.env)",
      "Read(**/.env)",
      "Bash(rm -rf:*)",
      "Bash(sudo:*)",
      "Bash(curl:*)"
    ]
  },
  "outputStyle": "outline-architect"
}
```

**Invalid fields to avoid:**
- `defaultMode` - Not supported in permissions
- `project`, `agents`, `workflow`, `integrations` - Use separate `project.json` for metadata
- Permission patterns like `Bash(curl:**/api/keys/**)` - The `:*` must be at the end only

**For complex projects**, create two files:
1. `settings.json` - Only valid Claude Code settings
2. `project.json` - Custom metadata about your project

This configuration automatically accepts file edits in the manuscript directory, asks before running Pandoc or committing, and denies reading sensitive files.

## **7. Hooks for Automation**

Hooks execute shell commands at key events (PreToolUse, PostToolUse, Notification, Stop). They ensure deterministic automation independent of Claude's memory.

**IMPORTANT: New Hook Format (Claude Code 1.0+)**

Hooks now require a matcher format with arrays. Here's the correct structure:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": {
          "tools": ["Edit"]
        },
        "hooks": [
          {
            "type": "command",
            "command": "proselint manuscript/*.md 2>/dev/null || true",
            "timeout": 30
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "cat manuscript/ch*.md > assets/full_manuscript.md",
            "timeout": 60
          }
        ]
      }
    ]
  }
}
```

**Note**: SubAgentStop is no longer valid. Use the events: PreToolUse, PostToolUse, Stop, SessionStart, SessionEnd.

For simpler setups, consider using a `settings-simple.json` without hooks to avoid validation errors.

## **8. Integrating External Tools via MCP**

The **Model Context Protocol (MCP)** lets Claude connect to external tools, databases and APIs. Anthropic's documentation notes that with MCP servers you can implement features from issue trackers, analyze monitoring data, query databases or integrate designs. For a writing toolkit, MCP servers extend Claude's capabilities beyond file I/O: [19](https://docs.claude.com/en/docs/claude-code/mcp#:~:text=What%20you%20can%20do%20with,MCP)

- **Research and web search** – Add a search MCP server (e.g. `brave-search` or `duckduckgo`) so sub‑agents can perform web queries and incorporate current information directly into drafts. [20](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=To%20add%20a%20new%20MCP,server%2C%20type%20this%20in)
- **Notion MCP** – The Notion MCP server provides secure access to a Notion workspace, enabling Claude to read and update pages. A developer experimenting with this integration reported that the MCP bridge reduces friction compared to manual copy‑pasting, although there can be issues with images and tables. [21](https://kareemf.com/claude-notion-mcp#:~:text=Anthropic%2C%20the%20company%20behind%20Claude%2C,Obsian%2C%20Apple%20Notes%2C%20and%20others)
- **Slack / Discord / Email** – Use MCP servers for Slack or email to send drafts for feedback or receive comments directly in the session.
- **Zen MCP** – A multi‑model orchestration server that allows Claude to consult other models (Gemini, O3, etc.) for brainstorming and consensus. Its features include multi‑model collaboration, automatic model selection and tools for deep reasoning, planning and consensus. You could create a workflow where the Outline Architect drafts a chapter, then Zen's consensus tool aggregates feedback from multiple models before finalising. [22](https://jimmysong.io/en/ai/zen-mcp-server/#:~:text=A%20server%20implementation%20of%20the,need%20to%20be%20truly%20helpful) [23](https://jimmysong.io/en/ai/zen-mcp-server/#:~:text=Zen%20MCP%20Server%20is%20a,solving%2C%20and%20collaborative%20development%20capabilities)

When adding MCP servers, choose an appropriate scope (project, user or global) and only install servers you trust. Use `claude mcp add` commands or edit `.mcp.json` to configure them. [24](https://docs.claude.com/en/docs/claude-code/mcp#:~:text=Here%20are%20some%20commonly%20used,can%20connect%20to%20Claude%20Code)

## **9. Headless Mode and Batch Scripts**

Headless mode (`claude -p "<prompt>"`) enables non‑interactive runs. Anthropic's best practices recommend it for CI/CD, hooks and automation. For writing, headless scripts can: [25](https://www.anthropic.com/engineering/claude-code-best-practices#:~:text=Claude%20Code%20includes%20headless%20mode,json%60%20for%20streaming%20JSON%20output)

- **Generate first drafts of all chapters** – loop through outline entries and call `/draft-chapter n` in headless mode, writing output to files.
- **Batch process revisions** – iterate over chapters and call `/revise-chapter n`.
- **Automate research updates** – call search MCP prompts regularly and incorporate new findings.

Use `--allowedTools` flags to specify tool access and `--output-format json` to parse results programmatically.

## **10. Project‑Level Context with Claude Projects**

Claude.ai's **Projects** feature allows you to curate knowledge and custom instructions in a web environment. Each project has a 200k‑token context window and can hold style guides, documents and past chats. You can define custom instructions to tailor Claude's responses. While this is separate from Claude Code, it complements a co‑authoring workflow: store research articles, world‑building documents and character biographies in a project, then ask your sub‑agents to reference them during drafting. Teams can share work products and inspiration through the project activity feed. [26](https://www.anthropic.com/news/projects#:~:text=200K%20context%20window%2C%20the%20equivalent,insights%20to%20enhance%20Claude%E2%80%99s%20effectiveness) [27](https://www.anthropic.com/news/projects#:~:text=In%20addition%2C%20you%20can%20define,and%20extend%20your%20skills%20further) [28](https://www.anthropic.com/news/projects#:~:text=Spark%20inspiration%20through%20sharing)

## **11. Best Practices and Additional Tips**

- **Iterative workflow** – Plan → Act → Review. Use Plan Mode for strategy, then Default or Auto Mode for execution, and delegate reviews to sub‑agents. [29](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Plan%20Mode%3A%20Strategic%20Thinking%20First) [30](https://www.siddharthbharath.com/claude-code-the-complete-guide/#:~:text=Usage%20Pattern%3A%20When%20you%20finish,filling%20up%20the%20context%20window)
- **Context management** – Keep CLAUDE.md concise and hierarchical. Use separate sub‑agents to prevent context bloat. Clear chat history with `/clear` or start new sessions when switching tasks.
- **Permission hygiene** – Grant only the permissions needed for writing tasks; deny potentially dangerous commands and environment reads.
- **File naming conventions** – Use versioning instead of status suffixes. For example: `ch01_title.md` → `ch01_title_v2.md` → `ch01_title_v3.md` rather than `ch01_draft.md` → `ch01_revised.md`
- **Agent completion messages** – Have agents report completion with file paths and statistics for better tracking
- **Project activation** – **CRITICAL**: Must start Claude Code from within the project directory for .claude/ settings to work
- **Research integration** – Combine search MCP servers with fact‑checking sub‑agents to ensure accuracy. Always treat external content as untrusted and verify claims.
- **Multi‑model collaboration** – Use Zen MCP for tasks that benefit from diverse perspectives, such as brainstorming plots or generating creative variations.
- **User roles** – Assign roles or personas in your superprompt to maintain consistency (e.g., "You are a developmental editor," "You are a marketer"). Sub‑agents can inherit these personas.
- **Exporting** – Use hooks to automatically generate PDF or EPUB outputs via Pandoc or reportlab after each major draft.

## **Conclusion**

By combining a well‑structured project, customised CLAUDE.md, tailor‑made output styles, specialised sub‑agents, custom slash commands, precise permissions, automated hooks and powerful MCP integrations, you can transform Claude Code into a comprehensive co‑authoring studio. This toolkit not only expands a seed note into a market‑ready manuscript but also automates research, editing, fact‑checking and marketing tasks. With thoughtful configuration and adherence to best practices, Claude becomes a true collaborator—handling the drudgery of writing while empowering you to focus on creativity and strategic decisions.

---

### **References**

- Cooking with Claude Code: The Complete Guide - Sid Bharath
  <https://www.siddharthbharath.com/claude-code-the-complete-guide/>

- Claude Code Best Practices | Anthropic
  <https://www.anthropic.com/engineering/claude-code-best-practices>

- Claude Code now lets you customize its communication style | AI Native Dev
  <https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style>

- Connect Claude Code to tools via MCP - Claude Docs
  <https://docs.claude.com/en/docs/claude-code/mcp>

- Integrating AI Tools with Notion: A Practical Experiment with Claude and Model Context Protocol
  <https://kareemf.com/claude-notion-mcp>

- Zen MCP Server | Jimmy Song
  <https://jimmysong.io/en/ai/zen-mcp-server/>

- Collaborate with Claude on Projects | Anthropic
  <https://www.anthropic.com/news/projects>


  ### Reference Descriptions

  Here is a reference list for the sources used in the report *Designing the Ultimate Claude Code Co‑Authoring Toolkit*.  Each link is given in full (not as Markdown), with a note about the relevant parts of the report it supports.

1. **Collaborate with Claude on Projects – Anthropic News (June 25 2024)** – This announcement introduces the *Projects* feature in Claude.ai.  It explains that projects have a 200 k‑token context window (equivalent to a 500‑page book) and allow users to store style guides, documents and past chats.  It also notes that you can define custom instructions for each project to tailor responses.
   [https://www.anthropic.com/news/projects](https://www.anthropic.com/news/projects)

2. **Cooking with Claude Code: The Complete Guide – Sid Bharath (July 8 2025, updated August 2025)** – A comprehensive guide to Claude Code that covers practically every feature: sub‑agents, plan→act→review workflows, git worktrees for multiple sessions, creating custom slash commands, using MCP servers, permissions, hooks and headless mode.  Sections cited include the benefits of separate sub‑agent context, how to create and edit sub‑agent definitions, the iterative plan→act→review pattern, using git worktrees for parallel Claude sessions, defining custom slash commands in `.claude/commands/`, connecting MCP servers for web search and other tools, and configuring hooks for automation.
   [https://siddharthbharath.com/claude-code-the-complete-guide/](https://siddharthbharath.com/claude-code-the-complete-guide/)

3. **Integrating AI Tools with Notion: A Practical Experiment with Claude and Model Context Protocol – Kareem F. (Dec 22 2024)** – A blog post describing how to connect Claude to Notion via an MCP server.  It highlights that using the Notion MCP bridge reduces friction compared to manual copy‑pasting but notes issues when transferring images and tables back to Notion.
   [https://kareemf.com/claude-notion-mcp](https://kareemf.com/claude-notion-mcp)

4. **Claude Code now lets you customize its communication style – AI Native Dev (Sept 4 2025)** – News article detailing Anthropic’s new *explanatory* and *learning* output styles, and how to switch them via `/output-style explanatory` or `/output-style learning`.  It also explains how to create custom output styles with `/output-style:new` and discusses the difference between output styles and sub‑agents.
   [https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style](https://ainativedev.io/news/claude-code-now-lets-you-customize-its-communication-style)

5. **Connect Claude Code to tools via MCP – Claude Docs** – Official documentation on connecting Claude Code to external tools with the Model Context Protocol.  It explains that MCP servers can implement features such as reading issues from trackers, analyzing monitoring data, querying databases and integrating design systems.  It also advises choosing an appropriate scope (local, project or user) when installing servers.
   [https://docs.claude.com/en/docs/claude-code/mcp](https://docs.claude.com/en/docs/claude-code/mcp)

6. **Claude Code: Best practices for agentic coding – Anthropic Engineering Blog (Apr 18 2025)** – Official guidance on using Claude Code effectively.  It recommends creating a `CLAUDE.md` file for project memory and detailing style guides and workflow conventions.  The article covers configuring permissions via `/permissions` or `.claude/settings.json`, iterating on `CLAUDE.md` as a living document, and using headless mode (`claude -p`) for CI/CD and automation.
   [https://www.anthropic.com/engineering/claude-code-best-practices](https://www.anthropic.com/engineering/claude-code-best-practices)

7. **Zen MCP Server – Jimmy Song (Jul 27 2025)** – Overview of the Zen MCP server, a multi‑model orchestration tool.  It notes that Zen allows AI assistants like Claude to collaborate with other models (e.g. Gemini for deep analysis, O3 for logic debugging) and supports features like multi‑model collaboration, automatic model selection, local model support and dynamic context.  The server also provides tools such as *chat*, *thinkdeep*, *planner* and *consensus* for consensus analysis and project planning.
   [https://jimmysong.io/en/ai/zen-mcp-server/](https://jimmysong.io/en/ai/zen-mcp-server/)

8. **Output styles – Claude Docs** – Documentation explaining how output styles work.  It clarifies that output styles modify Claude’s system prompt and lists the built‑in *explanatory* and *learning* styles.  It explains how to switch styles (`/output-style explanatory`), create new styles with `/output-style:new`, and contrasts output styles with `CLAUDE.md` and custom slash commands.  (Although this page isn’t explicitly footnoted in the report, it provides background on output styles and is relevant to the discussion.)
   [https://docs.claude.com/en/docs/claude-code/output-styles](https://docs.claude.com/en/docs/claude-code/output-styles)

These references collectively support the report’s recommendations on project structure, memory management, output styles, sub‑agents, custom commands, permissions, hooks, MCP integrations, headless mode and multi‑model collaboration.
