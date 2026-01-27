add_executable(mylib_example_basic
    basic_usage.cpp
)

target_link_libraries(mylib_example_basic
    PRIVATE
        mylib
)