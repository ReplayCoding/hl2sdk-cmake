add_library(
  mathlib

  color_conversion.cpp
  halton.cpp
  lightdesc.cpp
  mathlib_base.cpp
  powsse.cpp
  sparse_convolution_noise.cpp
  sseconst.cpp
  sse.cpp
  ssenoise.cpp
  3dnow.cpp
  anorms.cpp
  bumpvects.cpp
  IceKey.cpp
  imagequant.cpp
  polyhedron.cpp
  quantize.cpp
  randsse.cpp
  spherical.cpp
  simdvectormatrix.cpp
  vector.cpp
  vmatrix.cpp
  almostequal.cpp
)

target_compile_options(mathlib PUBLIC "${SDK_CFLAGS}")
target_compile_options(
  mathlib PRIVATE
  -Wno-narrowing # Can't do much about potentially broken code
  -msse
)

target_link_libraries(mathlib tier0)
target_include_directories(
  mathlib SYSTEM PUBLIC
  "${SDK_INCLUDES}"
  "${PROJECT_SOURCE_DIR}/public/mathlib"
)

add_library(sdk::mathlib ALIAS mathlib)
