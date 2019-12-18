# Definition of Macros
add_definitions(-D_CONSOLE)

file(GLOB SOURCE_FILES
    "src/*.c"
    "src/*.h"
)
# exclude some source files
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/libmain.c")
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/src/libyywrap.c")

# Add executable to build.
add_executable(win_flex
   ${SOURCE_FILES}
)

target_include_directories(win_flex PRIVATE "src")
target_compile_options(win_flex PRIVATE /sdl- /MP)

target_link_libraries(win_flex common_lib kernel32.lib user32.lib Ws2_32.lib)

install(TARGETS win_flex
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)
