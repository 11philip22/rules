---
paths:
  - "src/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "include/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
  - "tests/**/*.{cc,cpp,cxx,h,hh,hpp,hxx,ipp,inl}"
---

# C++ Testing

## Coverage Expectations

- When changing behavior, add or update the narrowest relevant test if a test seam exists. If you cannot add coverage, call out the gap explicitly.

## Test Design

- Prefer deterministic tests that isolate filesystem, time, network, and SDK behavior behind wrappers or fakes instead of relying on live external services.
- Test public behavior at module boundaries rather than private implementation details.
- Cover failure paths and edge cases, especially retries, timeouts, path handling, quota checks, resume behavior, and rotation flows.

## Test Data And Speed

- Use temporary directories and synthetic file trees for scanner and upload-queue behavior instead of relying on developer-specific paths.
- Keep tests fast and specific. Separate routine coverage from slower integration-style checks when both are needed.

## Test Runner

- Use CMake and CTest.

## Running Tests

```sh
cmake --build build && ctest --test-dir build --output-on-failure
```

## Coverage

```sh
cmake -DCMAKE_CXX_FLAGS="--coverage" -DCMAKE_EXE_LINKER_FLAGS="--coverage" ..
cmake --build .
ctest --output-on-failure
lcov --capture --directory . --output-file coverage.info
```

## Sanitizers

- Use sanitizers in CI.
- Example: `cmake -DCMAKE_CXX_FLAGS="-fsanitize=address,undefined" ..`

## Static Analysis

- Use `clang-tidy` for automated checks.
- Example: `clang-tidy --checks='*' src/*.cpp`
- Use `cppcheck` for additional analysis.
- Example: `cppcheck --enable=all src/`
