OpenCode Rules Repository
=========================

This repository contains Markdown rule files for the `opencode-rules` plugin.
The plugin reads these files and injects matching rules into agent system prompts.

What This Repo Contains
-----------------------

- `cpp/` for C++ rules
- `python/` for Python rules
- `docker/` for Docker and Compose rules
- `cmake/` for CMake rules

How `opencode-rules` Uses These Files
-------------------------------------

- Reads `.md` and `.mdc` files recursively from configured rule directories
- Treats files without frontmatter as unconditional rules
- Uses YAML frontmatter such as `globs`, `keywords`, `tools`, and `match` to decide when a rule applies

Recommended Use
---------------

- Put this repo, or a symlink to it, under `~/.config/opencode/rules/`
- Or copy selected files into a project's `.opencode/rules/` directory

Example:

  ln -s /path/to/this/repo ~/.config/opencode/rules

Rule Design Conventions In This Repo
------------------------------------

- Keep always-on rules short, principle-based, and cheap to inject
- Put specialized guidance in separate files with narrower matching
- Avoid long examples in broad rules; examples belong in docs or skills
- Prefer behavior-shaping rules over language tutorials or reference material

Current Structure
-----------------

- Broad default guidance lives in files such as `coding-style.md`, `patterns.md`, `security.md`, and `testing.md`
- More situational guidance is split into narrower files, for example `python/comprehensions-generators.md`

Notes
-----

- Hidden directories are excluded by the plugin
- Rule files are discovered recursively
- Frontmatter is optional, but omitted frontmatter means the rule is always included
