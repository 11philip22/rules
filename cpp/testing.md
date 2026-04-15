---
globs:
  - "src/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "include/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "tests/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
---

# C++ Testing

- When changing behavior, add or update the narrowest relevant test. If you cannot add coverage, call out the gap.
- Prefer deterministic tests with wrappers or fakes over live filesystem, time, network, or external services.
- Test public behavior at module boundaries rather than private implementation details.
- Cover relevant failure paths and edge cases for the behavior under change.
- Use temporary directories and synthetic test data instead of developer-specific paths.
- Keep tests fast and focused; separate routine coverage from slower integration checks when needed.
