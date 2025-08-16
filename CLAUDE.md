# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is an n8n automation repository containing workflow definitions and their documentation. The repository is designed to create, manage, and document n8n workflows for various automation tasks.

## Structure

- **Workflow Files**: Each workflow consists of two files in the root directory:
  - `WorkflowName.json`: The n8n workflow definition
  - `WorkflowName.md`: Requirements documentation explaining the workflow's purpose and functionality

Example structure:
```
/n8n-automation/
├── Grokニュース取得.json
├── Grokニュース取得.md
├── Grok→Obsidian.json
├── Grok→Obsidian.md
└── CLAUDE.md
```

## Working with n8n Workflows

### n8n MCP Tools

You have access to n8n MCP tools for building and validating workflows. When creating or modifying n8n workflows:

1. **Start with** `tools_documentation()` to understand available tools
2. **Use validation** throughout the process:
   - Pre-validate node configurations with `validate_node_minimal()` and `validate_node_operation()`
   - Post-validate complete workflows with `validate_workflow()`
3. **Prefer standard nodes** over Code nodes unless absolutely necessary
4. **Use diff operations** (`n8n_update_partial_workflow()`) for updates to save tokens

### Workflow Import Rule

**CRITICAL**: Always import JSON changes to n8n instance after updating workflow files:

1. **After any JSON modification**: Use `n8n_create_workflow()` or `n8n_update_full_workflow()` 
2. **Environment**: Import to Hostinger n8n instance (https://n8n.srv955997.hstgr.cloud)
3. **Validation**: Verify import success before considering task complete
4. **No exceptions**: This rule applies to ALL JSON workflow changes

### File Management Rules

When working with workflows:

1. **Markdown Requirements Documentation**: Always maintain `.md` files as the source of truth for requirements
2. **JSON-Markdown Sync**: Markdown content MUST accurately reflect the current JSON implementation
3. **Workflow File Structure**:
   ```
   /n8n-automation/
   ├── WorkflowName.json    # n8n workflow definition
   ├── WorkflowName.md      # Requirements documentation
   └── CLAUDE.md            # Repository guidelines
   ```
4. **File Naming**: Use consistent naming pattern where `.json` and `.md` files share the same base name

### Workflow Documentation Standards

When creating workflow documentation (`.md` files), focus on:

- **Purpose**: What problem does this workflow solve?
- **Requirements**: What are the functional requirements?
- **Data Flow**: How does information move through the workflow?
- **Customization Points**: What can be easily modified?
- **Use Cases**: Real-world scenarios where this workflow helps

Avoid technical implementation details unless specifically requested. Documentation should be accessible to non-technical users.

## Language Preference

- User interactions should be in Japanese (日本語)
- Technical consultations with o3 mcp should be in English
- Always fact-check implementation details with o3 mcp in English at the end of implementations

## Current Workflows

### Grokニュース取得
- **Purpose**: Weekly AI news aggregation from X (Twitter)
- **Schedule**: Every Saturday at 9 AM
- **Output**: Discord notifications with curated AI news
- **Key Features**: Filters by popularity (60+ likes), includes source URLs, auto-splits long messages
- **Status**: Legacy workflow (Discord output)

### Grok→Obsidian
- **Purpose**: Weekly AI news aggregation from X (Twitter) with Obsidian knowledge management
- **Schedule**: Every Saturday at 9 AM  
- **Output**: Structured Markdown files in GitHub repository for Obsidian
- **Key Features**: YAML frontmatter, internal links, tags, automatic file organization
- **GitHub Integration**: Creates files in `AI-News/YYYY-MM-DD-ai-weekly.md` format
- **Status**: Active workflow (Obsidian output)