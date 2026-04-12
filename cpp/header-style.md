---
globs:
  - "src/**/*.{h,hh,hpp,hxx}"
  - "include/**/*.{h,hh,hpp,hxx}"
  - "tests/**/*.{h,hh,hpp,hxx}"
---

# C++ Header Style

## Header Guards

- All project-owned headers must use traditional header guards, not #pragma once.
- Prefer guard macros derived from the header name in `UPPER_SNAKE_CASE`.
- Example:

```cpp
#ifndef MY_HEADER_H
#define MY_HEADER_H
```
