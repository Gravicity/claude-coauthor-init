# Designing the Ultimate Next.js Landing Page Co-Authoring Toolkit

## Introduction

Next.js is a powerful React framework for building modern web applications with features like server-side rendering, static site generation, and API routes. When combined with Claude Code's capabilities, we can create a comprehensive toolkit that accelerates landing page development through AI-assisted component generation, styling, optimization, and deployment. This report outlines a production-grade co-authoring toolkit specifically designed for rapidly building high-converting landing pages.

## 1. Project Scaffold

A well-structured Next.js landing page project separates components, styles, content, and configuration:

```
nextjs-landing/
├── src/
│   ├── app/              # Next.js 13+ app directory
│   ├── components/       # Reusable components
│   ├── lib/              # Utility functions
│   └── styles/           # Global styles and themes
├── public/               # Static assets
├── content/              # CMS/content files
├── tests/                # Test suites
├── .claude/
│   ├── commands/         # Custom commands
│   ├── agents/           # Specialized agents
│   ├── output-styles/    # Communication styles
│   ├── templates/        # Component templates
│   └── settings.json     # Permissions and hooks
├── PROJECT.md            # Project guidelines
└── package.json          # Dependencies
```

## 2. PROJECT.md – Project Memory

PROJECT.md serves as the development guidelines and memory for the Next.js project:

- **Tech Stack**: Next.js 14+, React, Tailwind CSS, TypeScript
- **Design System**: Color palette, typography, spacing scales
- **Component Standards**: Naming conventions, prop patterns, accessibility requirements
- **Performance Targets**: Core Web Vitals scores, bundle size limits
- **SEO Requirements**: Meta tags, structured data, sitemap generation
- **Deployment**: Vercel configuration, environment variables

## 3. Output Styles

Custom output styles for different development modes:

- **Component Architect**: Plans component hierarchy and prop interfaces
- **Style Engineer**: Creates Tailwind configurations and responsive designs
- **Performance Optimizer**: Analyzes bundles and suggests improvements
- **Content Strategist**: Writes compelling copy and CTAs
- **SEO Specialist**: Optimizes for search engines

## 4. Sub-Agents

### Component Builder
- Creates React components with TypeScript interfaces
- Implements responsive designs with Tailwind CSS
- Ensures accessibility (ARIA labels, keyboard navigation)
- Generates Storybook stories for components

### Style Designer
- Develops consistent design tokens
- Creates Tailwind configuration and custom utilities
- Implements dark mode support
- Manages CSS-in-JS when needed

### API Integrator
- Sets up API routes in Next.js
- Integrates with headless CMS (Contentful, Strapi)
- Implements form submissions and email services
- Handles authentication flows

### Performance Auditor
- Analyzes bundle sizes with webpack-bundle-analyzer
- Implements code splitting and lazy loading
- Optimizes images with next/image
- Monitors Core Web Vitals

### SEO Optimizer
- Generates meta tags and Open Graph data
- Creates structured data (JSON-LD)
- Implements sitemap and robots.txt
- Manages canonical URLs and redirects

## 5. Custom Commands

- `/create-section <type>` – Generate landing page sections (hero, features, testimonials)
- `/add-component <name>` – Create new reusable component with tests
- `/optimize-images` – Convert and optimize all images for web
- `/generate-theme` – Create consistent color and typography system
- `/audit-performance` – Run Lighthouse and provide recommendations
- `/deploy-preview` – Deploy to Vercel preview environment
- `/a11y-check` – Run accessibility audit
- `/extract-text` – Extract all text for translation/editing

## 6. Permissions and Settings

```json
{
  "permissions": {
    "allow": [
      "Read(src/**)",
      "Write(src/**)",
      "Edit(src/**)",
      "MultiEdit(src/**)",
      "Read(content/**)",
      "Write(content/**)",
      "Read(public/**)",
      "Write(public/**)",
      "TodoWrite"
    ],
    "ask": [
      "Bash(npm:*)",
      "Bash(pnpm:*)",
      "Bash(yarn:*)",
      "Bash(git:*)",
      "Bash(vercel:*)",
      "WebSearch",
      "WebFetch"
    ],
    "deny": [
      "Read(.env.local)",
      "Read(.env.production)",
      "Bash(rm -rf:*)",
      "Bash(sudo:*)"
    ]
  },
  "outputStyle": "component-architect"
}
```

## 7. Hooks for Automation

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": {
          "tools": ["Write", "Edit"]
        },
        "hooks": [
          {
            "type": "command",
            "command": "npm run lint:fix 2>/dev/null || true",
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
            "command": "npm run build && npm run export",
            "timeout": 120
          }
        ]
      }
    ]
  }
}
```

## 8. External Integrations (MCP)

Recommended MCP servers for Next.js development:

- **Figma MCP**: Import designs directly from Figma
- **Contentful MCP**: Manage headless CMS content
- **Vercel MCP**: Deploy and manage hosting
- **Analytics MCP**: Integrate Google Analytics, Plausible
- **Stripe MCP**: Add payment processing
- **Email MCP**: Set up transactional emails

## 9. Batch Scripts

### build-all-sections.sh
```bash
#!/bin/bash
# Generate all standard landing page sections
sections=("hero" "features" "testimonials" "pricing" "faq" "cta")
for section in "${sections[@]}"; do
  claude -p "/create-section $section"
done
```

### optimize-for-production.sh
```bash
#!/bin/bash
# Full production optimization
npm run lint:fix
npm run type-check
claude -p "/optimize-images"
claude -p "/audit-performance"
npm run build
npm run analyze
```

### deploy-and-test.sh
```bash
#!/bin/bash
# Deploy to preview and run tests
vercel --prod=false
npm run test:e2e
npm run lighthouse
```

## 10. Best Practices

- **Component-First Development**: Build reusable components before pages
- **Mobile-First Design**: Start with mobile layouts, enhance for desktop
- **Performance Budget**: Keep JavaScript under 200KB, FCP under 1.5s
- **Accessibility First**: WCAG 2.1 AA compliance minimum
- **Type Safety**: Use TypeScript for all components and utilities
- **Testing Strategy**: Unit tests for utils, integration tests for components
- **SEO by Default**: Every page needs meta tags and structured data
- **Incremental Static Regeneration**: Use ISR for dynamic content
- **Image Optimization**: Always use next/image with proper sizing
- **Error Boundaries**: Implement error handling at component level

## Domain-Specific Workflows

### Landing Page Creation Flow
1. **Discovery**: Define goals, target audience, key messages
2. **Structure**: Plan sections and information architecture
3. **Design**: Create component designs and style guide
4. **Development**: Build components and assemble pages
5. **Content**: Write copy and gather assets
6. **Optimization**: Performance, SEO, accessibility audits
7. **Testing**: Cross-browser, device, and user testing
8. **Deployment**: Preview, stakeholder review, production

### Component Development Pattern
1. Design component interface (props, state)
2. Create TypeScript types/interfaces
3. Build component with Tailwind styles
4. Add Storybook story for documentation
5. Write unit tests
6. Implement accessibility features
7. Optimize for performance

## Conclusion

This Next.js landing page toolkit transforms Claude Code into a comprehensive web development partner. It automates component generation, ensures consistent styling, optimizes performance, and manages deployments. The specialized agents handle everything from responsive design to SEO optimization, while custom commands streamline common workflows. With proper configuration and adherence to best practices, teams can build high-quality landing pages in a fraction of the traditional time.

---

*Note: This is an example domain report demonstrating how the domain-researcher agent would document toolkits for specific technologies. Actual implementations would be tailored to specific project requirements.*