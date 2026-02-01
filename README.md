# OpenGL Template

A minimal, modern C++ OpenGL project template with zero manual dependency installation. Uses CPM (CMake Package Manager) to automatically fetch GLFW and GLAD.

## Features

✨ **Zero manual dependency installation** - CPM handles GLFW and GLAD automatically  
✨ **Modern CMake practices** - Target-based linking, C++20 support  
✨ **Cross-platform** - Works on Linux, macOS, and Windows  
✨ **OpenGL 3.3 Core Profile** - Modern OpenGL ready  
✨ **Optional mise integration** - Automated build tasks and tool management

## Prerequisites

### Required for All Platforms

1. **CMake** (version 3.14 or higher)
   - Download from [cmake.org](https://cmake.org/download/)
   - Or install via package manager

2. **C++ Compiler with C++20 Support**
   - **Linux**: GCC 10+ or Clang 10+
   - **macOS**: Xcode Command Line Tools (Clang)
   - **Windows**: Visual Studio 2019+ or MinGW-w64

3. **Internet Connection** (first build only)
   - Required for CPM to download dependencies automatically

### Platform-Specific Requirements

#### Linux
```bash
# Ubuntu/Debian
sudo apt install build-essential cmake libx11-dev libxrandr-dev libxinerama-dev libxcursor-dev libxi-dev

# Fedora/RHEL
sudo dnf install gcc-c++ cmake libX11-devel libXrandr-devel libXinerama-devel libXcursor-devel libXi-devel
```

#### macOS
```bash
# Install Xcode Command Line Tools
xcode-select --install
```

#### Windows

**For most users with NVIDIA/AMD GPUs:** OpenGL drivers are included in your graphics driver package.

**If you encounter OpenGL initialization errors**, install the [OpenCL™, OpenGL®, and Vulkan® Compatibility Pack](https://apps.microsoft.com/detail/9nqpsl29bfff) from the Microsoft Store. This is commonly needed for:
- ARM-based Windows devices (Surface Pro X, etc.)
- Virtual machines
- Systems with incomplete GPU drivers
- Some laptops with integrated graphics only

### Optional: mise

[mise](https://mise.jdx.dev/) is a polyglot tool version manager that can automate build tasks and manage dependencies.

```bash
# Install mise (Linux/macOS)
curl https://mise.run | sh

# Install mise (Windows with PowerShell)
irm https://mise.run | iex
```

## Getting Started

### Option 1: Build with mise (Recommended)

If you have mise installed, it will automatically install CMake, Ninja, and Python:

```bash
# Build and run (Debug mode)
mise run

# Or use the alias
mise r

# Build and run (Release mode)
mise run:release

# Just build (Debug)
mise build

# Just build (Release)
mise build:release

# Clean build files
mise clean
```

### Option 2: Build with CMake (Standard)

#### Quick Start
```bash
# Create build directory
mkdir build
cd build

# Configure and build
cmake ..
cmake --build .

# Run the executable
./opengl-template       # Linux/macOS
.\opengl-template.exe   # Windows
```

#### Using the Custom Run Target
```bash
# Build and run in one command
cmake --build . --target run
```

#### Debug vs Release Builds
```bash
# Debug build (default)
cmake -B build/debug -DCMAKE_BUILD_TYPE=Debug
cmake --build build/debug
./build/debug/opengl-template

# Release build (optimized)
cmake -B build/release -DCMAKE_BUILD_TYPE=Release
cmake --build build/release
./build/release/opengl-template
```

#### Using Ninja (Faster Builds)
```bash
cmake -B build -G Ninja
cmake --build build
```

## Project Structure

```
opengl-template/
├── CMakeLists.txt      # CMake configuration with CPM
├── mise.toml           # mise task automation (optional)
├── src/
│   └── main.cpp        # Main OpenGL application
└── build/              # Generated build files (gitignored)
```

## Customization

1. **Change project name**: Edit `project(opengl-template ...)` in `CMakeLists.txt`
2. **Add source files**: Add them to `add_executable()` in `CMakeLists.txt`
3. **Add dependencies**: Use `CPMAddPackage()` to fetch more libraries

## Dependencies (Auto-downloaded)

- **GLFW 3.4** - Windowing and input handling
- **GLAD 2.0.8** - OpenGL function loader (Core Profile 3.3)
- **CPM.cmake 0.42.1** - CMake package manager

## Troubleshooting

### "Failed to initialize GLAD" Error

**On Windows**: Install the [OpenGL Compatibility Pack](https://apps.microsoft.com/detail/9nqpsl29bfff) from Microsoft Store

**On Linux**: Ensure you have proper graphics drivers installed:
```bash
# Check OpenGL version
glxinfo | grep "OpenGL version"
```

**On macOS**: Update to the latest macOS version and Xcode

### CMake Cannot Find OpenGL

Make sure you have graphics drivers installed. On Linux, you may need mesa development files:
```bash
sudo apt install libgl1-mesa-dev  # Ubuntu/Debian
sudo dnf install mesa-libGL-devel # Fedora/RHEL
```

## License

This template is released under the MIT License. Feel free to use it for any project!

---

**Need help?** Open an issue on GitHub or check the [GLFW documentation](https://www.glfw.org/docs/latest/) and [OpenGL tutorials](https://learnopengl.com/).