cmake_minimum_required(VERSION 3.10)
project(my_crow_project)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add executable
add_executable(my_crow_server main.cpp)

# Include Crow header file
target_include_directories(my_crow_server PRIVATE include)

# Check if running on Linux
if (UNIX)
    message(STATUS "Configuring for Linux")

    # Find ASIO (either standalone or system-wide)
    find_path(ASIO_INCLUDE_DIR asio.hpp PATHS /usr/include /usr/local/include)

    if (ASIO_INCLUDE_DIR)
        message(STATUS "ASIO found in ${ASIO_INCLUDE_DIR}")
        target_include_directories(my_crow_server PRIVATE ${ASIO_INCLUDE_DIR})
        target_link_libraries(my_crow_server PRIVATE pthread)
    else()
        message(FATAL_ERROR "ASIO not found. Please install ASIO or Boost.Asio.")
    endif()
endif()

# Link with pthread (if using MinGW)
if (MINGW)
    target_link_libraries(my_crow_server pthread)
endif()
