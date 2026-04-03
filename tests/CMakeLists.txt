include(FetchContent)

FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG v1.15.2
)

set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(googletest)

add_executable(mylib_tests
    test_foo.cpp
)

target_link_libraries(mylib_tests
    PRIVATE
        mylib::mylib
        GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(mylib_tests)
