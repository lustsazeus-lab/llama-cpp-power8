# Contributing to llama.cpp for IBM POWER8

Thank you for your interest in contributing! This document provides guidelines for contributing to this project.

## Prerequisites

### Build Requirements

- **Operating System**: Ubuntu 20.04 LTS (last POWER8-supported release)
- **Compiler**: GCC with POWER8 support
- **Build Tool**: CMake 3.14 or higher
- **Hardware**: IBM POWER8 server (optional for development, required for testing)

### Required Compiler Flags

```bash
-mcpu=power8 -mvsx -maltivec -O3 -mtune=power8 -funroll-loops
```

### Optional Dependencies

- **IBM MASS Library**: For optimized math functions (`libmassvp8`, `libmass`)
- **OpenMP**: Enabled via `-DGGML_OPENMP=ON`

## Development Workflow

### 1. Fork and Clone

```bash
git clone https://github.com/YOUR_USERNAME/llama-cpp-power8
cd llama-cpp-power8
```

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
```

### 3. Make Changes

Ensure your code follows the POWER8-specific requirements:
- Use AltiVec/VSX intrinsics for vector operations
- Test with `-mcpu=power8` compiler flags
- Avoid x86_64-specific optimizations

### 4. Build and Test

```bash
# Configure
mkdir build && cd build
cmake .. \
    -DCMAKE_BUILD_TYPE=Release \
    -DGGML_OPENMP=ON \
    -DCMAKE_C_FLAGS="-mcpu=power8 -mvsx -maltivec -O3 -mtune=power8 -funroll-loops" \
    -DCMAKE_CXX_FLAGS="-mcpu=power8 -mvsx -maltivec -O3 -mtune=power8 -funroll-loops"

# Build
make -j$(nproc)

# Run benchmarks
./altivec_benchmark
```

### 5. Submit a Pull Request

1. Push your branch to your fork
2. Open a PR against the `main` branch
3. Describe your changes and testing performed
4. Wait for review

## Testing Guidelines

- Test on actual POWER8 hardware when possible
- If you don't have POWER8 hardware, test compilation with cross-compilation tools
- Include benchmark results comparing before/after changes
- Verify no regressions in existing functionality

## Code Style

- Follow existing code conventions in the project
- Add comments for POWER8-specific optimizations
- Document any new build requirements

## Reporting Issues

- Use GitHub Issues for bug reports
- Include system information (OS, hardware)
- Provide reproduction steps
- Attach relevant logs

## License

By contributing, you agree that your contributions will be licensed under the project's license.
