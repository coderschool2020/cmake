cmake_minimum_required(VERSION 3.10)
project(Greeter)

# variables
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED on)
set(CMAKE_BUILD_TYPE Debug)
# ..or
# set(CMAKE_BUILD_TYPE Release)

# adding a library
set(SOURCES 
greeter.cpp
person.cpp
)
add_library(${PROJECT_NAME}-lib STATIC ${SOURCES})

# compiling driver code...
add_executable(${PROJECT_NAME} main.cpp)
# and linking with a library
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)

# compiling unit tests...
add_executable(${PROJECT_NAME}-ut test/greeter.ut.cpp)
# and linking with a library
target_link_libraries(${PROJECT_NAME}-ut ${PROJECT_NAME}-lib)

# compile options
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)
target_compile_options(${PROJECT_NAME}-ut PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)
target_compile_options(${PROJECT_NAME}-lib PRIVATE -Wall -Wextra -Werror -pedantic -Wconversion -O3)

# tests launch
enable_testing()
add_test(NAME MyTest COMMAND ${PROJECT_NAME}-ut)
