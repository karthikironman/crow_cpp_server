cmake_minimum_required(VERSION 3.10)
project(my_crow_project)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add executable
add_executable(my_crow_server main.cpp)

# Include Crow header file
target_include_directories(my_crow_server PRIVATE include)

# Link with pthread (if using MinGW)
if (MINGW)
    target_link_libraries(my_crow_server pthread)
endif()