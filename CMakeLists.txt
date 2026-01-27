cmake_minimum_required(VERSION 3.14)

# Replace the project name with your desired name
project(opengl-template LANGUAGES C CXX)
set(CMAKE_CXX_STANDARD 20)

# --- 1. BOOTSTRAP CPM (The "No Manual Download" part) ---
set(CPM_DOWNLOAD_VERSION 0.42.1)
set(CPM_DOWNLOAD_LOCATION "${CMAKE_BINARY_DIR}/cmake/CPM_${CPM_DOWNLOAD_VERSION}.cmake")

if(NOT EXISTS "${CPM_DOWNLOAD_LOCATION}")
    message(STATUS "Downloading CPM.cmake to ${CPM_DOWNLOAD_LOCATION}")
    file(DOWNLOAD
         https://github.com/cpm-cmake/CPM.cmake/releases/download/v${CPM_DOWNLOAD_VERSION}/CPM.cmake
         "${CPM_DOWNLOAD_LOCATION}"
    )
endif()
include("${CPM_DOWNLOAD_LOCATION}")

# --- 2. FETCH DEPENDENCIES ---

# Fetch GLFW (Windowing)
CPMAddPackage(
    NAME glfw
    GITHUB_REPOSITORY glfw/glfw
    GIT_TAG 3.4
    OPTIONS
        "GLFW_BUILD_DOCS OFF"
        "GLFW_BUILD_EXAMPLES OFF"
        "GLFW_BUILD_TESTS OFF"
        "GLFW_INSTALL OFF"
)

# Fetch GLAD (OpenGL Loader)
CPMAddPackage(
    NAME glad
    GITHUB_REPOSITORY Dav1dde/glad
    VERSION 2.0.8
    DOWNLOAD_ONLY YES
)

if(glad_SOURCE_DIR)
    add_subdirectory(${glad_SOURCE_DIR}/cmake glad-cmake)
    glad_add_library(glad STATIC REPRODUCIBLE LOADER LANGUAGE C API gl:core=3.3)
endif()

find_package(OpenGL REQUIRED)

add_executable(${PROJECT_NAME} src/main.cpp)

# Target-based linking (Modern Best Practice)
target_link_libraries(${PROJECT_NAME} PRIVATE
    glfw
    glad
    OpenGL::GL
)

# Handle Linux-specific math library requirement if necessary
if(UNIX AND NOT APPLE)
    target_link_libraries(${PROJECT_NAME} PRIVATE m)
endif()

add_custom_target(run
    COMMAND "${PROJECT_NAME}"
    WORKING_DIRECTORY "${CMAKE_PROJECT_DIR}"
    USES_TERMINAL
)
