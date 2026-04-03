add_executable(mylib_bin
    main.cpp
)

target_link_libraries(mylib_bin
    PRIVATE
        mylib::mylib
)

target_include_directories(main
    PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)
