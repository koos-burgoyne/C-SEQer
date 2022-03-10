# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
cmake_minimum_required(VERSION 3.12)

# project name
project (
    c-seqer
    HOMEPAGE_URL https://github.com/koos-burgoyne/C-SEQer
)

set(CMAKE_CXX_STANDARD 11)

set(
    HPP_FILES
    
    src/DeNovo.hpp
    src/Dictionary.hpp
    src/DiGraph.hpp
    src/main_functions.hpp
    src/MGF.hpp
)
set(
    CPP_FILES

    src/C-SEQER.cpp
)

# Add an executable
add_executable(
    c-seqer
    ${CPP_FILES}
)