# WEWEI's Coding Prompts

This is a repo for my personal coding prompts, neutral to different projects.

## Repository Structure

- `languages/` - Prompts for different programming languages
- `scenarios/` - Prompts for different scenarios
- `roles/` - Prompts for different roles

## Purpose

This repository contains project-neutral coding prompts that can be used across different programming tasks. Organize your prompts by programming language, scenario type, or role-specific context.

## Configuring VS Code to Use These Prompts

To configure VS Code to use these prompts with GitHub Copilot:

### Configure VS Code Settings

1. In VS Code, go to Settings (File > Preferences > Settings or `Ctrl+,`)
2. Search for "prompt files"
3. Find "Chat: Prompt Files" setting
4. Add the path to this repository
5. Or create/edit your `settings.json` file to include:

```json
{
  "chat.promptFiles": [
    "/path/to/wewei-coding-prompts"
  ]
}
```

After configuring, you can access your prompts in Copilot Chat by using the `/prompt` command followed by the filename without the extension.
