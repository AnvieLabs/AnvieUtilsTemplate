cmake_minimum_required(VERSION 3.5)

# replace AnvTemplate and anvtemplate with your project name
project(AnvTemplate VERSION 0 LANGUAGES C)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# add extra warnings, and address sanitizer
# comment this out before release
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror -fsanitize=address")

# add include_directory calls to include submodule headers
add_subdirectory(Modules)

# link all targets to anvutils_headers, providing access to
# Anvie Utils headers to every source file within project.
link_libraries(anvutils_headers)

# create an executable
add_executable(anvtemplate Source/Main.c)
target_link_libraries(anvtemplate anvutils_containers)
