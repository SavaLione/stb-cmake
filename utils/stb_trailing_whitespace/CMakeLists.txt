cmake_minimum_required (VERSION 3.17)

project(stb_trailing_whitespace
    LANGUAGES C
)

add_executable(${PROJECT_NAME} src/trailing_whitespace.c)

target_link_libraries(${PROJECT_NAME} stb)

if(STB_INSTALL)
    install(
        TARGETS ${PROJECT_NAME}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    )
endif()