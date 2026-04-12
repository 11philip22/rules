---
globs:
  - "src/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "include/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "tests/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
---

# C++ Patterns

## Ownership And APIs

- Use RAII; do not use manual `new`/`delete` or `malloc`/`free`.
- Express ownership in types: prefer values and references, use `std::unique_ptr` for exclusive ownership, and `std::shared_ptr` only for shared ownership.
- Prefer `std::make_unique` and `std::make_shared` over raw `new`.
- Treat raw pointers as non-owning views unless an external API requires a different boundary.
- Pass cheap scalars by value. Pass read-only strings and buffers as `std::string_view`, `std::span`, or `const&`. Use output parameters only when an external API requires them.
- Keep invalid states hard to represent; prefer small focused types over sentinels or parallel containers.
- Keep headers self-sufficient and minimal; prefer forward declarations in headers and full definitions in translation units.

## Project Structure

- Preserve architectural boundaries.
- Keep orchestration in high-level modules and dependency-specific code in adapters or wrappers.
- Do not let high-level code bypass those interfaces to call low-level dependencies directly.
- When the repository defines explicit layering rules elsewhere, follow those rules.

## Standard Library Preference

- Use `std::chrono` for timeouts.
- Use `std::filesystem` for paths.

## Concurrency Patterns

- Keep callbacks and notification handlers light; hand off heavy work and return promptly.
- Prefer `std::jthread` for long-running worker threads and `std::stop_token` for cooperative cancellation.
- Keep lock scope tight and document which shared state a mutex or atomic protects.
- Use atomics only for small independent state transitions; protect multi-field invariants with a mutex.
- Do not let exceptions cross thread boundaries; catch them there and convert them into explicit results, errors, or logs.
- Do not add clever template or metaprogramming machinery unless it materially simplifies a real constraint in this codebase.
