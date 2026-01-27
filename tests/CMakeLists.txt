# Tests for mylib

include(FetchContent)

# Install GoogleTest
FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/refs/tags/v1.15.2.zip
)

# For MSVC
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(googletest)

# To be supplemented
add_executable(mylib_tests
    test_foo.cpp
)

target_link_libraries(mylib_tests
    PRIVATE
        mylib
        GTest::gtest_main
)

# CTest
include(GoogleTest)
gtest_discover_tests(mylib_tests)