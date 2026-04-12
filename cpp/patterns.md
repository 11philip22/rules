---
paths:
  - "src/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "include/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "tests/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
---

# C++ Patterns

## Ownership And APIs

- Use RAII everywhere. Do not use manual `new` or `delete`.
- Use `std::unique_ptr` for exclusive ownership.
- Use `std::shared_ptr` only when shared ownership is truly needed.
- Use `std::make_unique` and `std::make_shared` over raw `new`.
- Use C++ allocation and object lifetime management instead of `malloc` or `free`.
- Treat raw pointers as non-owning views unless a required external API forces a different boundary.
- Express ownership and lifetime in types: prefer values, references, `std::unique_ptr`, and `std::shared_ptr` only when ownership is genuinely shared.
- Pass cheap scalar types by value. Pass read-only string or buffer inputs as `std::string_view`, `std::span`, or `const&` as appropriate. Use output parameters only when an external API forces that shape.
- Keep invalid states hard to represent. Prefer small focused types over loosely-related fields, sentinel values, or parallel containers.
- Keep headers self-sufficient and minimal. Prefer forward declarations in headers when possible, and include full definitions in translation units that need them.

## Project Structure

- Preserve the project's architectural boundaries.
- Keep orchestration in high-level modules and dependency-specific code in dedicated adapter
or wrapper layers.
- Do not let high-level code bypass those interfaces to call low-level dependencies directly.
- When the repository defines explicit layering rules elsewhere, follow those rules.

## Standard Library Preference

- Use `std::chrono` for timeouts.
- Use `std::filesystem` for paths.
- Use `std::regex` for confirmation-link extraction.

## Concurrency Patterns

- Keep callbacks and notification handlers lightweight; hand off heavyweight work and return promptly.
- Prefer `std::jthread` for long-running worker threads and `std::stop_token` for cooperative cancellation.
- Keep lock scope tight and document which shared state a mutex or atomic protects.
- Use atomics only for small independent state transitions; protect multi-field invariants with a mutex.
- Do not let exceptions cross thread boundaries; catch them at the boundary and convert them into explicit results, errors, or logs.
- Do not add clever template or metaprogramming machinery unless it materially simplifies a real constraint in this codebase.
