add_executable(__PROJECT_NAME_BIN__
    main.cpp
)

target_link_libraries(__PROJECT_NAME_BIN__
    PRIVATE
        __PROJECT_NAME__
)

target_include_directories(__PROJECT_NAME_BIN__
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)

set_target_properties(__PROJECT_NAME_BIN__ PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
    OUTPUT_NAME "main"
)
