# CMake 最低版本要求（兼容你的环境，3.15+ 均可）
cmake_minimum_required(VERSION 3.15)

# 项目名称（目标程序名：VisualSort）
project(VisualSort)

# 设置 C++ 标准（C++17，和之前一致）
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# -------------------------- 1. 配置头文件路径 --------------------------
# 1.1 SDL2 头文件路径（和你之前的配置一致，不变）
include_directories(D:\\vscodecpp\\x86_64-w64-mingw32\\include)
# 1.2 自定义源码头文件路径（src 目录下的 .h/.hpp 文件，必须加！）
include_directories(${PROJECT_SOURCE_DIR}/src)

# -------------------------- 2. 配置库文件路径 --------------------------
# SDL2 库文件路径（和你之前的配置一致，不变）
link_directories(D:\\vscodecpp\\SDL2-devel-2.30.7-mingw\\SDL2-2.30.7\\x86_64-w64-mingw32\\lib)

# -------------------------- 3. 关键：指定 src 目录下的源文件 --------------------------
# 方式1：如果 src 下只有 1 个主文件（比如 main.cpp），直接写路径
# add_executable(VisualSort ${PROJECT_SOURCE_DIR}/src/main.cpp)

# 方式2：如果 src 下有多个 .cpp 文件（推荐！自动找所有 src 下的 .cpp）
file(GLOB_RECURSE SOURCES ${PROJECT_SOURCE_DIR}/src/*.cpp)
add_executable(VisualSort ${SOURCES})

# -------------------------- 4. 链接依赖库 --------------------------
# SDL2 链接顺序（mingw32 → SDL2main → SDL2，顺序不能乱）
target_link_libraries(VisualSort 
    mingw32
    SDL2main
    SDL2
)

# 隐藏控制台黑框（GUI 程序必备，和之前的 -mwindows 效果一致）
set(CMAKE_EXE_LINKER_FLAGS "-mwindows")