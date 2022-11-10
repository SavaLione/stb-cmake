cmake_minimum_required (VERSION 3.17)

project(stb
    LANGUAGES C
	VERSION 1.0.0
	DESCRIPTION "Unofficial CMake implementation of the stb libraries"
	HOMEPAGE_URL "https://github.com/savalione/stb-cmake"
)

include(GNUInstallDirs)

# Determine if stb is built as a subproject (using add_subdirectory)
# or if it is the master project.
if(NOT DEFINED STB_MASTER_PROJECT)
	set(STB_MASTER_PROJECT OFF)
	if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
    	set(STB_MASTER_PROJECT ON)
    	message(STATUS "CMake version: ${CMAKE_VERSION}")
  	endif ()
endif ()

option(STB_INSTALL "Generate the install target" ${STB_MASTER_PROJECT})

option(STB_BUILD_STB_CONNECTED_COMPONENTS "Build stb_connected_components library (incrementally compute reachability on grids)" ON)
option(STB_BUILD_STB_C_LEXER "Build stb_c_lexer library (simplify writing parsers for C-like languages)" ON)
option(STB_BUILD_STB_DIVIDE "Build stb_divide library (more useful 32-bit modulus e.g. \"euclidean divide\")" ON)
option(STB_BUILD_STB_DS "Build stb_ds library (typesafe dynamic array and hash tables for C, will compile in C++)" ON)
option(STB_BUILD_STB_DXT "Build stb_dxt library (Fabian \"ryg\" Giesen's real-time DXT compressor)" ON)
option(STB_BUILD_STB_EASY_FONT "Build stb_easy_font library (quick-and-dirty easy-to-deploy bitmap font for printing frame rate, etc)" ON)
option(STB_BUILD_STB_HERRINGBONE_WANG_TILE "Build stb_herringbone_wang_tile library (herringbone Wang tile map generator)" ON)
option(STB_BUILD_STB_HEXWAVE "Build stb_hexwave library (audio waveform synthesizer)" ON)
option(STB_BUILD_STB_IMAGE "Build stb_image library (image loading/decoding from file/memory: JPG, PNG, TGA, BMP, PSD, GIF, HDR, PIC)" ON)
option(STB_BUILD_STB_IMAGE_RESIZE "Build stb_resize library (resize images larger/smaller with good quality)" ON)
option(STB_BUILD_STB_IMAGE_WRITE "Build stb_write library (image writing to disk: PNG, TGA, BMP)" ON)
option(STB_BUILD_STB_INCLUDE "Build stb_include library (implement recursive #include support, particularly for GLSL)" ON)
option(STB_BUILD_STB_LEAKCHECK "Build stb_leakcheck library (quick-and-dirty malloc/free leak-checking)" ON)
option(STB_BUILD_STB_PERLIN "Build stb_perlin library (perlin's revised simplex noise w/ different seeds)" ON)
option(STB_BUILD_STB_RECT_PACK "Build stb_rect_pack library (simple 2D rectangle packer with decent quality)" ON)
option(STB_BUILD_STB_SPRINTF "Build stb_sprintf library (fast sprintf, snprintf for C/C++)" ON)
option(STB_BUILD_STB_TEXTEDIT "Build stb_textedit library (guts of a text editor for games etc implementing them from scratch)" ON)
option(STB_BUILD_STB_TILEMAP_EDITOR "Build stb_tilemap_editor library (embeddable tilemap editor)" ON)
option(STB_BUILD_STB_TRUETYPE "Build stb_truetype library (parse, decode, and rasterize characters from truetype fonts)" ON)
option(STB_BUILD_STB_VORBIS "Build stb_vorbis library (decode ogg vorbis files from file/memory to float/16-bit signed output)" ON)
option(STB_BUILD_STB_VOXEL_RENDER "Build stb_voxel_render library (Minecraft-esque voxel rendering \"engine\" with many more features)" ON)

option(STB_BUILD_DEPRECATED "Build deprecated libraries" OFF)
option(STB_BUILD_DEPRECATED_RRSPRINTF "Build single file sprintf replacement (rrsprintf.h)" ON)
option(STB_BUILD_DEPRECATED_STB "Build Sean's Tool Box (stb.h)" ON)
option(STB_BUILD_DEPRECATED_STRETCHY_BUFFER "Build a vector<>-like dynamic array for C (stretchy_buffer.h)" ON)

option(STB_BUILD_UTILS "Build utils" OFF)
option(STB_BUILD_UTIL_STB_BUILD_MATRIX "Build util build_matrix.c" ON)
option(STB_BUILD_UTIL_STB_EASY_FONT_MAKER "Build util easy_font_maker that was used to encode the data for stb_simple_font.h" ON)
option(STB_BUILD_UTIL_STB_MAKE_README "Build util make_readme.c" ON)
option(STB_BUILD_UTIL_STB_TRAILING_WHITESPACE "Build util trailing_whitespace.c" ON)
option(STB_BUILD_UTIL_STB_UNICODE "Build util that create unicode mappings" ON)

# Set default build to release
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose Release or Debug build type" FORCE)
endif()

message(STATUS "Build type: " ${CMAKE_BUILD_TYPE})

set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

add_library(${PROJECT_NAME} INTERFACE)

add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})


if(STB_INSTALL)
	install(
		TARGETS ${PROJECT_NAME}
		EXPORT ${PROJECT_NAME}Targets
		LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
		ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
		RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
		INCLUDES DESTINATION "include"
	)

	install(
		EXPORT "${PROJECT_NAME}Targets"
		FILE "${PROJECT_NAME}Targets.cmake"
		NAMESPACE "${PROJECT_NAME}::"
		DESTINATION "lib/cmake/${PROJECT_NAME}"
	)

	target_link_libraries(${PROJECT_NAME} INTERFACE
		rrsprintf::rrsprintf
		stb_lib::stb_lib
		stretchy_buffer::stretchy_buffer
		stb_connected_components::stb_connected_components
		stb_c_lexer::stb_c_lexer
		stb_divide::stb_divide
		stb_ds::stb_ds
		stb_dxt::stb_dxt
		stb_easy_font::stb_easy_font
		stb_herringbone_wang_tile::stb_herringbone_wang_tile
		stb_hexwave::stb_hexwave
		stb_image::stb_image
		stb_image_resize::stb_image_resize
		stb_image_write::stb_image_write
		stb_include::stb_include
		stb_leakcheck::stb_leakcheck
		stb_perlin::stb_perlin
		stb_rect_pack::stb_rect_pack
		stb_sprintf::stb_sprintf
		stb_textedit::stb_textedit
		stb_tilemap_editor::stb_tilemap_editor
		stb_truetype::stb_truetype
		stb_vorbis::stb_vorbis
		stb_voxel_render::stb_voxel_render
	)
endif()

add_subdirectory(src)

if(STB_BUILD_UTILS)
	add_subdirectory(utils)
endif()