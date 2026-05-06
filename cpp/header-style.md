---
globs:
  - "src/**/*.{h,hh,hpp,hxx}"
  - "include/**/*.{h,hh,hpp,hxx}"
  - "tests/**/*.{h,hh,hpp,hxx}"
agent:
  - build
  - cpp-reviewer
match: all
---

# C++ Header Style

## Header Guards

- All project-owned headers must use header guards, not `#pragma once`.
- Prefer guard macros derived from the header name in `UPPER_SNAKE_CASE`.
