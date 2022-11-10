cmake_minimum_required (VERSION 3.17)

project(stb_divide
    VERSION 0.94
    LANGUAGES C
)

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(${PROJECT_NAME} INTERFACE "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include>" "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>")

add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

if(STB_INSTALL)
    install(
		TARGETS ${PROJECT_NAME}
        EXPORT "stbTargets"
		LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
		ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
		RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
		INCLUDES DESTINATION "include"
	)

    install(
        EXPORT "stbTargets"
        FILE "stbTargets.cmake"
        NAMESPACE ${PROJECT_NAME}::
        DESTINATION "cmake/"
	)

    install(FILES "include/stb_divide.h" DESTINATION "include")
endif()