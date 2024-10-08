# Software Architecture with C++
Software Architecture with C++ by Packt Publishing

## Chapter 5: Leveraging C++ Language Features

### Prerequisites

Install the following software:

- CMake 3.15
- Conan 1.62.0
- GCC 13

Assuming you're on Linux or using WSL, configure a sacpp Conan profile and remotes by running:

```bash
conan profile new sacpp || true
conan profile update settings.compiler=gcc sacpp
conan profile update settings.compiler.libcxx=libstdc++11 sacpp
conan profile update settings.compiler.version=11 sacpp
conan profile update settings.arch=x86_64 sacpp
conan profile update settings.os=Linux sacpp
```

If GCC 13 is not your default compiler, you also need to add:

```bash
conan profile update env.CXX=`which g++-13` sacpp
conan profile update env.CC=`which gcc-13` sacpp
```

### Building

To build the project, first cd to its directory, and then run:

```bash
# This works but still spews a lot of outputs on the current directory, that shoulb be in their own dedicated directory.
mkdir build
cd build
conan install .. --build=missing -s build_type=Release -pr=sacpp
cd ..
cmake . -DCMAKE_BUILD_TYPE=Release # build type must match Conan's
cmake --build .
```

If GCC is not your default compiler, you can tell CMake to use it with the `CMAKE_CXX_COMPILER` flag.
Replace the first invocation above with:

```bash
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_COMPILER=`which g++-13`
```
