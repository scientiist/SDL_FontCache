cmake_minimum_required(VERSION 3.1)
project(SDL_FontCache VERSION 0.10.0 LANGUAGES C)

find_package(SDL2 REQUIRED)
find_package(SDL2_ttf REQUIRED)

include_directories(SDL_FontCache ${SDL2_INCLUDE_DIRS})
include_directories(SDL_FontCache ${SDL2_TTF_INCLUDE_DIRS})

#find_path(sdl2_INCLUDE_DIR SDL.h)
#find_library(sdl2_LIBRARY SDL2)
#find_library(sdl2main_LIBRARY SDL2main)
#find_path(sdl2_ttf_INCLUDE_DIR SDL_ttf.h)
#find_library(sdl2_ttf_LIBRARY SDL2_ttf)


#if (NOT sdl2_INCLUDE_DIR)
#    message(FATAL_ERROR "SDL2 include dir not found")
#endif()
#if (NOT sdl2_LIBRARY)
#    message(FATAL_ERROR "SDL2 library dir not found")
#endif()
#if (NOT sdl2main_LIBRARY)
#    message(FATAL_ERROR "SDL2main library dir not found")
#endif()
#if (NOT sdl2_ttf_INCLUDE_DIR)
#    message(FATAL_ERROR "SDL2_TTF include dir not found")
#endif()
#if (NOT sdl2_ttf_LIBRARY)
#    message(FATAL_ERROR "SDL2_TTF library dir not found")
#endif()


add_library(FontCache
		SDL_FontCache.h
		SDL_FontCache.c
		)

target_include_directories(FontCache PUBLIC .)
target_include_directories(FontCache PUBLIC ${SDL2_INCLUDE_DIRS})
target_include_directories(FontCache PUBLIC ${SDL2_TTF_INCLUDE_DIRS})
target_link_libraries(FontCache PUBLIC -lm SDL2 SDL2_ttf SDL2_image)
#target_link_libraries(FontCache ${sdl2main_LIBRARY})
#target_include_directories(FontCache PUBLIC ${sdl2_ttf_INCLUDE_DIR})
#target_link_libraries(FontCache ${sdl2_ttf_LIBRARY})

add_executable(FontCache-tests
		test/main.c
		)
file(COPY test/utf8_sample.txt DESTINATION ${CMAKE_BINARY_DIR})
file(COPY test/fonts/FreeSans.ttf DESTINATION ${CMAKE_BINARY_DIR}/fonts)
target_link_libraries(FontCache-tests FontCache)


