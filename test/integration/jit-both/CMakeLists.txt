cmake_minimum_required(VERSION 3.16)
project(jit)

enable_testing()

set(jit_HALIDE_VERSION ""
    CACHE STRING "Optional version argument to find_package(Halide)")

find_package(Halide ${jit_HALIDE_VERSION} REQUIRED static shared)

add_executable(main-shared main.cpp)
target_link_libraries(main-shared PRIVATE Halide::shared::Halide)

add_executable(main-static main.cpp)
target_link_libraries(main-static PRIVATE Halide::static::Halide)

add_test(NAME validate-shared COMMAND main-shared)
set_tests_properties(validate-shared PROPERTIES PASS_REGULAR_EXPRESSION "Success!")

add_test(NAME validate-static COMMAND main-static)
set_tests_properties(validate-static PROPERTIES PASS_REGULAR_EXPRESSION "Success!")
