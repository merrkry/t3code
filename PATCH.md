# PATCH.md

Here we document the changes we carry on top of upstream in this fork.

## Goal

This is a customized fork for personal use.

For maintainability, the scope of changes should stay limited, and we only target `x86_64-linux` for now.

## Workflow

This fork rebases onto upstream occasionally.

Only the intention and scope of the changes are documented here: what the problems are, and how we want to solve them.
This information should stay relatively stable over time.

Concrete implementation details should be documented in commit messages.
That information may change as upstream evolves.

Agents should resolve merge conflicts, port, or even rewrite these changes when relevant upstream code moves around.
This document, as well as the commit messages, should be updated accordingly.

## Changes

In this section, each title corresponds to a commit message, and main text describes the changes.

### docs: init PATCH.md

This fork rebases onto upstream occasionally, so future agents need a stable description of why these patches exist and what scope should be preserved.

See `Workflow` section above for detailed guidelines.

### web: disable composer spellcheck

Spellcheck works poorly for prompts, code, commands, and paths. Frequent false positives are distracting.

Disable spellcheck in the main composer input.

### desktop: add Window menu fallback on non-macOS

Electron's native Window menu behavior on Linux could consume `Ctrl+W` as close-window before the renderer handled it as terminal-close.

Use a simpler non-macOS Window menu that does not steal renderer shortcuts, while keeping the native menu behavior on macOS.

### ci: configure fork release workflows

Upstream release automation assumes upstream infrastructure and workflows that do not match this fork.

- Use standard GitHub-hosted runners with the default GitHub token.
- Publish nightly builds from branch `prod` under tag `nightly`. Linux artifacts only.

### desktop: disable custom title bar on Linux

The custom title bar setup does not play well with server-side decorations on Linux, especially under tiling window managers.

Keep Linux on the default native title bar path.

### server: allow disabling provider update checks

Provider harness update checks can create distracting update affordances and unnecessary background network traffic in this fork.

Allow `T3CODE_DISABLE_PROVIDER_UPDATE_CHECK` to suppress provider latest-version checks and update-available UI derived from those checks.
