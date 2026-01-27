# Needs to be supplemented with other files
add_library(mylib
    foo.cpp
)

target_include_directories(mylib
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
        $<INSTALL_INTERFACE:include>
)

# C++20 standart
target_compile_features(mylib PUBLIC cxx_std_20)

# Warnings
if (MSVC)
    target_compile_options(mylib PRIVATE /W4 /permissive-)
else()
    target_compile_options(mylib PRIVATE -Wall -Wextra -Wpedantic)
endif()