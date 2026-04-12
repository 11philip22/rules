---
globs:
  - "src/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "include/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "tests/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
---

# C++ Coding Style

## Naming Conventions

- Types and classes use `PascalCase`.
- Enum members use `PascalCase`.
- Functions and methods use `snake_case`.
- Local variables and function parameters use `snake_case`.
- Namespace-scope `constexpr` and `const` variables use `UPPER_SNAKE_CASE`.
- Namespaces are always `lowercase`.
- Member variables use `snake_case_` with a trailing underscore.

## Formatting

- Use `clang-format` for formatting.
- Run `clang-format -i <file>` before committing.

## Language Features

- Prefer modern C++ features over C-style constructs.
- Prefer standard library facilities over custom utilities unless a wrapper around a required dependency is the point of the code.
- Prefer `enum class`, `constexpr`, `constinit`, `[[nodiscard]]`, and `noexcept` when they make contracts clearer and prevent mistakes.
- Use `auto` when the initializer is clear; keep explicit types for ownership, narrowing, and API boundaries.
- Use structured bindings for pair-like values, e.g. `auto [key, value] = map_entry;`.
- Prefer range-based `for` and standard algorithms over index-heavy or stateful loops when readability improves.

## Readability

- Comment invariants, protocol quirks, lifetime constraints, and concurrency assumptions; do not restate the code.
- Avoid C-style casts and preprocessor macros for constants or simple helpers.
