OpenCode Rules Repository
=========================

This repository contains Markdown rule files for the `opencode-rules`
plugin. The plugin discovers these files, matches them against the active
workspace, and injects the applicable guidance into agent system prompts.

Contents
--------

- `cpp/` - C++ style, naming, headers, patterns, testing, and security
- `rust/` - Rust style, patterns, testing, and security
- `python/` - Python style, patterns, testing, security, and comprehensions
- `cmake/` - CMake project and target best practices
- `docker/` - Dockerfile and Docker Compose rules

How The Plugin Uses These Files
-------------------------------

- Reads `.md` and `.mdc` files recursively from configured rule directories
- Ignores hidden directories
- Uses YAML frontmatter such as `globs`, `agent`, and `match` to decide when
  a rule applies
- Treats files without frontmatter as unconditional rules

Recommended Use
---------------

Put this repo, or a symlink to it, under the OpenCode rules directory:

  ln -s /path/to/this/repo ~/.config/opencode/rules

For project-specific guidance, copy only the relevant files into:

  .opencode/rules/

Rule Design
-----------

- Keep broad rules short, principle-based, and cheap to inject
- Put specialized guidance in separate files with narrower matching
- Prefer behavior-shaping rules over language tutorials or reference material
- Avoid long examples in broad rules; examples belong in docs or skills
- Match rules with `globs` whenever the guidance only applies to specific
  languages, tools, or file types

Current Structure
-----------------

- `coding-style.md` covers formatting, naming, and language conventions
- `patterns.md` covers design and implementation preferences
- `testing.md` covers test structure and expectations
- `security.md` covers defensive coding and common risk areas
- Narrow files, such as `cpp/file-names.md` and
  `python/comprehensions-generators.md`, cover situational guidance

References
----------

- https://github.com/affaan-m/everything-claude-code/tree/main/rules
