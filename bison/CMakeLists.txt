# Definition of Macros
add_definitions(-D_CONSOLE)

file(GLOB SOURCE_FILES
    "src/*.c"
    "src/*.h"
)
# exclude some source files
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/scan-code.c")
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/scan-gram.c")
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/scan-skel.c")


# Add executable to build.
add_executable(win_bison
   ${SOURCE_FILES}
)

target_include_directories(win_bison PRIVATE "src")
target_include_directories(win_bison PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_options(win_bison PRIVATE /sdl- /MP)

target_link_libraries(win_bison common_lib kernel32.lib user32.lib)

install(TARGETS win_bison
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)
