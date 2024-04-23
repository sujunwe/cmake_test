cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

# 把生成的动态库、exe文件都指定到bin目录
# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# set(EXECUTABLE_OUTPUT_PATH 则不再使用
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
# 静态库使用命令
# set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY)
# linux 平台使用这个命令
# set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/dir)


aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_FILES)
# 把源文件生成动态库common
add_library(common 
SHARED
${SRC_FILES}
)
# 动态库包含所依赖的头文件
target_include_directories(common
PUBLIC
${PROJECT_SOURCE_DIR}/include)

# 可执行文件
add_executable(
    planning_main
    planning_main.cpp
)
# 生成的可执行文件也要链接头文件
target_include_directories(planning_main
PUBLIC
${PROJECT_SOURCE_DIR}/include)
# 生成的可执行文件也要链接上一步生成的动态库
target_link_libraries(planning_main
PUBLIC
common)