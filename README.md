# stb-cmake
This is an unofficial CMake implementation of the [stb](https://github.com/nothings/stb) libraries.

Libraries version:
|Library                    |Version|
|:--------------------------|:------|
|stb_c_lexer                |0.12   |
|stb_divide                 |0.94   |
|stb_dxt                    |1.12   |
|stb_herringbone_wang_tile  |0.7    |
|stb_image                  |2.27x  |
|stb_image_resize           |0.97   |
|stb_image_write            |1.16   |
|stb_leakcheck              |0.6    |
|stb_rect_pack              |1.01   |
|stb_textedit               |1.14   |
|stb_truetype               |1.26   |
|stb_voxel_render           |0.89   |
|stb_connected_components   |0.96   |
|stb_ds                     |0.67   |
|stb_easy_font              |1.1    |
|stb_hexwave                |0.5    |
|stb_include                |0.02   |
|stb_perlin                 |0.5    |
|stb_sprintf                |1.10   |
|stb_tilemap_editor         |0.42   |
|stb_vorbis                 |1.22   |

## Install
Just add and link the library to your CMake project:
```
add_subdirectory(stb-cmake)

target_link_libraries(${PROJECT_NAME} stb)
```

Or make install target:
```sh
$ git clone https://github.com/SavaLione/stb-cmake
$ cd stb-cmake
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_INSTALL_PREFIX=stb
$ make install
```

### Build options
* ``STB_BUILD_STB_CONNECTED_COMPONENTS``       (default:``ON``): Build stb_connected_components library (incrementally compute reachability on grids)
* ``STB_BUILD_STB_C_LEXER``                    (default:``ON``): Build stb_c_lexer library (simplify writing parsers for C-like languages)
* ``STB_BUILD_STB_DIVIDE``                     (default:``ON``): Build stb_divide library (more useful 32-bit modulus e.g. \"euclidean divide\")
* ``STB_BUILD_STB_DS``                         (default:``ON``): Build stb_ds library (typesafe dynamic array and hash tables for C, will compile in C++)
* ``STB_BUILD_STB_DXT``                        (default:``ON``): Build stb_dxt library (Fabian \"ryg\" Giesen's real-time DXT compressor)
* ``STB_BUILD_STB_EASY_FONT``                  (default:``ON``): Build stb_easy_font library (quick-and-dirty easy-to-deploy bitmap font for printing frame rate, etc)
* ``STB_BUILD_STB_HERRINGBONE_WANG_TILE``      (default:``ON``): Build stb_herringbone_wang_tile library (herringbone Wang tile map generator)
* ``STB_BUILD_STB_HEXWAVE``                    (default:``ON``): Build stb_hexwave library (audio waveform synthesizer)
* ``STB_BUILD_STB_IMAGE``                      (default:``ON``): Build stb_image library (image loading/decoding from file/memory: JPG, PNG, TGA, BMP, PSD, GIF, HDR, PIC)
* ``STB_BUILD_STB_IMAGE_RESIZE``               (default:``ON``): Build stb_resize library (resize images larger/smaller with good quality)
* ``STB_BUILD_STB_IMAGE_WRITE``                (default:``ON``): Build stb_write library (image writing to disk: PNG, TGA, BMP)
* ``STB_BUILD_STB_INCLUDE``                    (default:``ON``): Build stb_include library (implement recursive #include support, particularly for GLSL)
* ``STB_BUILD_STB_LEAKCHECK``                  (default:``ON``): Build stb_leakcheck library (quick-and-dirty malloc/free leak-checking)
* ``STB_BUILD_STB_PERLIN``                     (default:``ON``): Build stb_perlin library (perlin's revised simplex noise w/ different seeds)
* ``STB_BUILD_STB_RECT_PACK``                  (default:``ON``): Build stb_rect_pack library (simple 2D rectangle packer with decent quality)
* ``STB_BUILD_STB_SPRINTF``                    (default:``ON``): Build stb_sprintf library (fast sprintf, snprintf for C/C++)
* ``STB_BUILD_STB_TEXTEDIT``                   (default:``ON``): Build stb_textedit library (guts of a text editor for games etc implementing them from scratch)
* ``STB_BUILD_STB_TILEMAP_EDITOR``             (default:``ON``): Build stb_tilemap_editor library (embeddable tilemap editor)
* ``STB_BUILD_STB_TRUETYPE``                   (default:``ON``): Build stb_truetype library (parse, decode, and rasterize characters from truetype fonts)
* ``STB_BUILD_STB_VORBIS``                     (default:``ON``): Build stb_vorbis library (decode ogg vorbis files from file/memory to float/16-bit signed output)
* ``STB_BUILD_STB_VOXEL_RENDER``               (default:``ON``): Build stb_voxel_render library (Minecraft-esque voxel rendering \"engine\" with many more features)

The remaining options deprecated and are not recommended for use.
* ``STB_BUILD_DEPRECATED``                    (default:``OFF``): Build deprecated libraries
* ``STB_BUILD_DEPRECATED_RRSPRINTF``           (default:``ON``): Build single file sprintf replacement (rrsprintf.h)
* ``STB_BUILD_DEPRECATED_STB``                 (default:``ON``): Build Sean's Tool Box (stb.h)
* ``STB_BUILD_DEPRECATED_STRETCHY_BUFFER``     (default:``ON``): Build a vector<>-like dynamic array for C (stretchy_buffer.h)

The remaining options do not affect the stb library proper, but only the sample applications (as ``stb_build_matrix``) are also not recommended for use.
* ``STB_BUILD_UTILS``                         (default:``OFF``): Build utils
* ``STB_BUILD_UTIL_STB_BUILD_MATRIX``          (default:``ON``): Build util build_matrix.c
* ``STB_BUILD_UTIL_STB_EASY_FONT_MAKER``       (default:``ON``): Build util easy_font_maker that was used to encode the data for stb_simple_font.h
* ``STB_BUILD_UTIL_STB_MAKE_README``           (default:``ON``): Build util make_readme.c
* ``STB_BUILD_UTIL_STB_TRAILING_WHITESPACE``   (default:``ON``): Build util trailing_whitespace.c
* ``STB_BUILD_UTIL_STB_UNICODE``               (default:``ON``): Build util that create unicode mappings

## Additional information
* Author of this unofficial CMake implementation: Saveliy Pototskiy ([savalione.com](https://savalione.com))
* Link to Github: https://github.com/SavaLione/stb-cmake
* Date of creation: 2022-11-10