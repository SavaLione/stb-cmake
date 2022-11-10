cmake_minimum_required (VERSION 3.17)

project(stb_make_readme
    LANGUAGES C
)

add_executable(${PROJECT_NAME} src/make_readme.c)

target_link_libraries(${PROJECT_NAME} stb)

if(STB_INSTALL)
    install(
        TARGETS ${PROJECT_NAME}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    )

    install(FILES "assets/README.footer.md" DESTINATION "bin/assets")
    install(FILES "assets/README.header.md" DESTINATION "bin/assets")
    install(FILES "assets/README.list" DESTINATION "bin/assets")
    install(FILES "assets/README.md" DESTINATION "bin/assets")
endif()