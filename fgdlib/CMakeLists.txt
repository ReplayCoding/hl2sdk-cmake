add_library(
  fgdlib

  gamedata.cpp
  gdclass.cpp
  gdvar.cpp
  inputoutput.cpp
  wckeyvalues.cpp
)

target_compile_options(fgdlib PUBLIC "${SDK_CFLAGS}")
target_compile_options(
  fgdlib PRIVATE
  -Wno-write-strings
)

target_link_libraries(fgdlib tier0 tier1)
target_include_directories(
  fgdlib SYSTEM PUBLIC
  "${SDK_INCLUDES}"
  "${PROJECT_SOURCE_DIR}/public/fgdlib"
  "${PROJECT_SOURCE_DIR}/utils/common"
)

add_library(sdk::fgdlib ALIAS fgdlib)
