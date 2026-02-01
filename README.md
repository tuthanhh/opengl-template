# OpenGL Template

A minimal, modern C++ OpenGL project template with zero manual dependency installation. Uses CPM (CMake Package Manager) to automatically fetch GLFW and GLAD.

## Prerequisites

### Required for All Platforms

1. **CMake** (version 3.14 or higher)
   - Download from [cmake.org](https://cmake.org/download/)
   - Or install via package manager

2. **C++ Compiler with C++20 Support**
   - **Linux**: GCC 10+ or Clang 10+
   - **macOS**: Xcode Command Line Tools (Clang)
   - **Windows**: Visual Studio 2019+ or MinGW-w64


3. **Python 3.x with jinja2** (for GLAD code generation)  
   - GLAD 2.x uses Python and jinja2 to generate OpenGL loader code  
   - **If using mise**: Automatically handled  
   - **If using standard CMake**: Install manually:  
   
   ```bash
   # Check if Python is installed
   python --version  # or python3 --version  
   
   # Install jinja2
   pip install jinja2  # or pip3 install jinja2


4. **Internet Connection** (first build only)
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
cmake -S . -B build
cmake --build build

# Run the executable
./build/opengl-template       # Linux/macOS
./build\opengl-template.exe   # Windows
```

#### Using the Custom Run Target
```bash
# Replace `cmake --build build` and manually run the executable
cmake --build build --target run
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
