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
- Constants use `UPPER_SNAKE_CASE`. This applies to all `constexpr` and `const` variables at namespace scope.
- Namespaces are always `lowercase`.
- Member variables use `snake_case_` with a trailing underscore.

## Formatting

- Use `clang-format` for formatting. No style debates.
- Run `clang-format -i <file>` before committing.

## Language Features

- Prefer modern C++ features over C-style constructs.
- Prefer standard library facilities over custom utilities unless a wrapper around a required dependency is the point of the code.
- Prefer expressive standard types such as `std::string_view`, `std::span`, `std::optional`, and `std::variant` when they clarify ownership or intent.
- Prefer `enum class`, `constexpr`, `constinit`, `[[nodiscard]]`, and `noexcept` when they make contracts clearer and prevent mistakes.
- Use auto for local variables when the initializer directly shows the type, such as constructor calls, casts, or iterator-returning expressions. Prefer explicit types when they make ownership, narrowing, or API boundaries clearer.
- Use structured bindings when unpacking pair-like values, for example `auto [key, value] = map_entry;`.
- Prefer range-based `for` and standard algorithms over index-heavy or stateful loops when readability improves.

## Readability

- Keep comments focused on invariants, protocol quirks, lifetime constraints, or concurrency assumptions. Do not add comments that simply restate the code.
- Avoid C-style casts and preprocessor macros for constants or simple helpers.
