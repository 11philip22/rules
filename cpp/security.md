---
globs:
  - "src/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "include/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "tests/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
---

# C++ Security

## Trust Boundaries

- Treat CLI input, environment variables, filesystem paths, email contents, network responses, and SDK data as untrusted. Validate and normalize them at module boundaries before use.

## Memory Safety

- Prefer `std::array` and `std::vector` over C-style arrays.
- Avoid `reinterpret_cast` unless absolutely necessary.

## Buffer Safety

- Prefer `std::string` and standard-library containers over raw character buffers.
- Use `.at()` for bounds-checked access when safety matters.
- Never use `strcpy`, `strcat`, or `sprintf`; use `std::string` or `fmt::format`.

## Undefined Behavior

- Always initialize variables.
- Avoid signed integer overflow.
- Never dereference null or dangling pointers.

## Sensitive Data

- Do not log or print secrets such as passwords, session tokens, confirmation links, or raw mailbox contents. Redact sensitive values in diagnostics and reports.

## Defensive Implementation

- Prefer explicit bounds, overflow, and narrowing checks when working with sizes, handles, indexes, counts, and byte math.
- Preserve exception safety. Prefer local temporaries and commit-at-end updates so failures do not leave partially-mutated state behind.
- Surface failures with actionable messages that include the operation and stable identifiers, but do not leak sensitive data.
- Swallow errors only for clearly documented best-effort cleanup paths.
