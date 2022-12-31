cmake_minimum_required(VERSION 3.10)
project(source-sdk-2013)

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
 add_compile_options (-fdiagnostics-color=always)
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
 add_compile_options (-fcolor-diagnostics)
endif ()

set(
  SDK_CFLAGS

  -DGNUC
  -DCOMPILER_GCC
  -D_LINUX -DLINUX
  -DPOSIX -D_POSIX
  -DNO_HOOK_MALLOC -DNO_MALLOC_OVERRIDE
  -DUSE_SDL -DDX_TO_GL_ABSTRACTION
  -DRAD_TELEMETRY_DISABLED
  -D_GLIBCXX_USE_CXX11_ABI=0
  # This is annoying but otherwise there are warnings
  -Wno-non-virtual-dtor
  -Wno-unused-parameter
)

set(
  SDK_INCLUDES

  "${PROJECT_SOURCE_DIR}/public"
  "${PROJECT_SOURCE_DIR}/common"
  "${PROJECT_SOURCE_DIR}/game/shared"
  "${PROJECT_SOURCE_DIR}/game/client"
  "${PROJECT_SOURCE_DIR}/game/server"
  "${PROJECT_SOURCE_DIR}"
)

function(get_compiled_lib name type)
  set(LIB_SUFFIX "")
  if(type STREQUAL STATIC)
    set(LIB_SUFFIX ".a")
  endif()
  find_library(
    LIBRARY_${name}
    NAMES ${name}${LIB_SUFFIX}
    PATHS
      ${PROJECT_SOURCE_DIR}/fixed-libs
      ${PROJECT_SOURCE_DIR}/lib/public/linux32
    NO_DEFAULT_PATH REQUIRED)
  set(
    INCLUDES_${name}

    "${SDK_INCLUDES}"
    "${PROJECT_SOURCE_DIR}/public/${name}"
  )

  add_library(${name} ${type} IMPORTED GLOBAL)
  target_include_directories(${name} SYSTEM INTERFACE ${INCLUDES_${name}})
  set_target_properties(
    ${name} PROPERTIES
    IMPORTED_LOCATION "${LIBRARY_${name}}"
  )
  add_library(sdk::${name} ALIAS ${name})
endfunction()

get_compiled_lib(tier0 SHARED)

add_subdirectory(tier1)
add_subdirectory(mathlib)
add_subdirectory(fgdlib)

get_compiled_lib(tier2 STATIC)
get_compiled_lib(tier3 STATIC)
get_compiled_lib(bitmap STATIC)
