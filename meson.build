project('source-sdk-2013', 'cpp', default_options : [
  'warning_level=3',
  'werror=true',
])
cxx = meson.get_compiler('cpp')

sdk_cflags = [
  '-DGNUC',
  '-DCOMPILER_GCC',
  '-D_LINUX', '-DLINUX',
  '-DPOSIX', '-D_POSIX',
  '-DNO_HOOK_MALLOC', '-DNO_MALLOC_OVERRIDE',
  '-DUSE_SDL', '-DDX_TO_GL_ABSTRACTION',
  '-D_GLIBCXX_USE_CXX11_ABI=0',

  # This is annoying but otherwise there are warnings
  '-Wno-non-virtual-dtor',
  '-Wno-unused-parameter',
]
sdk_libdirs = [
  meson.current_source_dir() / 'fixed-libs',
  meson.current_source_dir() / 'lib/public/linux32'
]
sdk_headers = include_directories(
  'public',
  'common',
  '.',

  # Don't let warnings propagate out of the SDK
  is_system: true,
)

# we build tier1 ourselves
prebuilt_lib_names = ['tier0', 'tier2', 'tier3', 'bitmap']
prebuilt_deps = {}

# These aren't included in the SDK as source code
# tier0 is a shared lib so we need to fixup the soname
# we will also need to do this for vstdlib if
# we ever use it.
foreach name: prebuilt_lib_names
  prebuilt_deps += {name: declare_dependency(
    compile_args: sdk_cflags,
    include_directories: include_directories('./public' / name),
    dependencies: [
      cxx.find_library(name, dirs: sdk_libdirs),
    ]
  )}
endforeach

subdir('tier1')

prebuilt_dep_list = []
foreach name, dep: prebuilt_deps
  prebuilt_dep_list += dep
endforeach

sdk_dep = declare_dependency(
  compile_args: sdk_cflags,
  dependencies: [tier1_dep] + prebuilt_dep_list,
  include_directories: sdk_headers,
)
