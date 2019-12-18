# Definition of Macros
add_definitions(-D_LIB)

file(GLOB SOURCE_FILES
    "misc/*.c"
	"misc/*.h"
    "misc/bitset/*.c"
	"misc/bitset/*.h"
	"m4/*.c"
	"m4/*.h"
	"m4/lib/*.c"
	"m4/lib/*.h"
)
# exclude some source files
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/m4/lib/regexec.c")
list(REMOVE_ITEM SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/m4/lib/regcomp.c")

# Add library to build.
add_library(common_lib STATIC
   ${SOURCE_FILES}
)

target_include_directories(common_lib PUBLIC "misc")
target_include_directories(common_lib PUBLIC "m4")
target_include_directories(common_lib PUBLIC "m4/lib")
target_compile_options(common_lib PRIVATE /sdl- /MP)

install(TARGETS common_lib
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
)

