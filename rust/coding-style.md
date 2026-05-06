---
globs:
  - "**/*.rs"
agent:
  - build
  - rust-reviewer
match: all
---

# Rust Coding Style

## Formatting

- Use the repo's configured formatter and linter; if unspecified, run `cargo fmt` and `cargo clippy -- -D warnings`.
- Follow rustfmt defaults, including 4-space indentation and 100-column line width.

## Immutability

- Use `let` by default; use `let mut` only when mutation is required.
- Prefer returning new values over mutating in place.
- Use `Cow<'_, T>` when a function may or may not need to allocate.

## Naming

- Use `snake_case` for functions, methods, variables, modules, and crates.
- Use `PascalCase` for types, traits, enums, and type parameters.
- Use `SCREAMING_SNAKE_CASE` for constants and statics.
- Use short lowercase lifetimes such as `'a` and `'de'`; use descriptive names only when needed.

## Ownership And Borrowing

- Borrow by default; take ownership only when the value must be stored or consumed.
- Do not clone just to satisfy the borrow checker without understanding why.
- Accept `&str` over `String` and `&[T]` over `Vec<T>` in function parameters.
- Use `impl Into<String>` for constructors that need owned strings.

## Error Handling

- Use `Result<T, E>` and `?` for propagation; do not use `unwrap()` in production code.
- In libraries, prefer typed errors such as `thiserror`; in applications, prefer `anyhow` for flexible context.
- Add context with `.with_context(...)` when it improves diagnostics.
- Prefer `Option` and `Result` combinators over deeply nested `match` blocks when they make the code clearer.
- Reserve `unwrap()` and `expect()` for tests and truly unreachable states.

## API Contracts

- Mark important return values `#[must_use]` when ignoring them is likely a bug.

## Control Flow

- Prefer iterator chains for transformations; use loops for complex control flow.

## Visibility

- Default to private; use `pub(crate)` for internal sharing.
- Mark `pub` only for real public API.
- Re-export the public API from `lib.rs`.
