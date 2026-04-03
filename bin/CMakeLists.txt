add_executable(mylib_bin
    main.cpp
)

target_link_libraries(mylib_bin
    PRIVATE
        mylib
)

target_include_directories(mylib_bin
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)

set_target_properties(mylib_bin PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
    OUTPUT_NAME "main"
)
