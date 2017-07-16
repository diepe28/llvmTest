cmake_minimum_required(VERSION 3.7)
project(llvmTest)

find_package(LLVM REQUIRED CONFIG)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

set(CMAKE_CXX_STANDARD 11)

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})

set(SOURCE_FILES main.cpp)
add_executable(llvmTest ${SOURCE_FILES})

# Find the libraries that correspond to the LLVM components
# that we wish to use
llvm_map_components_to_libnames(llvm_libs support core irreader linker mcjit x86 x86codegen)

# Link against LLVM libraries
target_link_libraries(llvmTest ${llvm_libs})