---
globs:
  - "CMakeLists.txt"
  - "**/CMakeLists.txt"
  - "*.cmake"
  - "**/*.cmake"
agent:
  - build
  - cpp-reviewer
match: all
---

# CMake Best Practices

## Project Setup

- Call `cmake_minimum_required()` at the top level and keep the version aligned with the features used.
- Call `project()` once at the root and keep enabled languages minimal and explicit.
- Keep top-level configuration declarative; move repeated logic into `cmake/` modules or small local functions.
- Set policies intentionally; do not silence warnings by forcing old behavior without a documented reason.

## Target-Based Design

- Prefer target-based CMake; model build outputs as targets and configure them with `target_*` commands.
- Use `target_sources()`, `target_link_libraries()`, `target_include_directories()`, `target_compile_definitions()`, and `target_compile_options()` instead of directory-wide state.
- Scope usage requirements correctly with `PRIVATE`, `PUBLIC`, and `INTERFACE`.
- Prefer imported targets from `find_package()` over raw library paths, hand-built include paths, or plain library variables.
- Avoid `include_directories()`, `link_directories()`, `link_libraries()`, `add_definitions()`, and global `add_compile_options()` for normal target configuration.

## Dependencies And Options

- Use `find_package()` for external dependencies and link imported targets directly.
- Use `option()` for user-facing booleans; keep cache variable names consistent and project-prefixed when appropriate.
- Validate required inputs at configure time and fail with clear `message(FATAL_ERROR ...)` diagnostics.
- Avoid mutating `CMAKE_CXX_FLAGS` and other global flags for normal target configuration; prefer target-specific options unless the project has a documented exception.

## Sources And Paths

- List sources explicitly; avoid `file(GLOB ...)` unless automatic regeneration is intentional.
- Keep generated files and configure outputs in the build tree, not the source tree.
- Prefer `CMAKE_CURRENT_SOURCE_DIR`, `CMAKE_CURRENT_BINARY_DIR`, and `cmake_path()` over ad hoc relative-path string manipulation.

## Reusable CMake Code

- Prefer `function()` over `macro()` unless macro semantics are specifically required.
- Keep helper modules idempotent, narrow in scope, and named for one responsibility.
- Use `cmake_parse_arguments()` for keyword-style helper functions when it improves clarity.
- Keep generator expressions minimal; use them only when configuration depends on target, toolchain, or build configuration.

## Testing And Installation

- Use `include(CTest)` and `add_test(NAME ... COMMAND ...)` for tests.
- When install rules are needed, prefer `GNUInstallDirs` and target-based `install(TARGETS ...)` or `install(FILES ...)`.
- Keep test and install logic close to the targets they describe.

## Diagnostics And Maintenance

- Fail early with concrete, actionable error messages when required tools, files, or inputs are missing.
- Use `message(STATUS ...)` for high-signal configure output and avoid noisy logs.
- Keep the build readable: short functions, clear target names, and one obvious place for each concern.
