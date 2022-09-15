tier1_sources = files(
  'bitbuf.cpp',
  'newbitbuf.cpp',
  'byteswap.cpp',
  'characterset.cpp',
  'checksum_crc.cpp',
  'checksum_md5.cpp',
  'checksum_sha1.cpp',
  'commandbuffer.cpp',
  'convar.cpp',
  'datamanager.cpp',
  'diff.cpp',
  'generichash.cpp',
  'ilocalize.cpp',
  'interface.cpp',
  'KeyValues.cpp',
  'kvpacker.cpp',
  'lzmaDecoder.cpp',
  # "lzss.cpp" [!$SOURCESDK]
  'mempool.cpp',
  'memstack.cpp',
  'NetAdr.cpp',
  'splitstring.cpp',
  # "processor_detect.cpp" [$WINDOWS||$X360]
  
  # [$POSIX]
  'processor_detect_linux.cpp',
  
  # [$LINUXALL||$PS3]
  'qsort_s.cpp',

  'rangecheckedvar.cpp',
  'reliabletimer.cpp',
  'stringpool.cpp',
  'strtools.cpp',
  'strtools_unicode.cpp',
  'tier1.cpp',
  'tokenreader.cpp',
  'sparsematrix.cpp',
  'uniqueid.cpp',
  'utlbuffer.cpp',
  'utlbufferutil.cpp',
  'utlstring.cpp',
  'utlsymbol.cpp',
  'utlbinaryblock.cpp',

  # [$LINUXALL]
  'pathmatch.cpp',

  'snappy.cpp',
  'snappy-sinksource.cpp',
  'snappy-stubs-internal.cpp',
)

tier1_cflags = [
  '-Wno-pedantic',
  '-Wno-implicit-fallthrough',
  '-Wno-register',
  '-Wno-sign-compare',
  '-Wno-reorder',
  '-Wno-misleading-indentation',
  '-Wno-nonnull-compare',
  '-Wno-strict-aliasing',
  '-Wno-unused-function',
  '-Wno-unused-result',
  '-Wno-unused-value',
  '-Wno-volatile',
  '-Wno-class-memaccess',
  '-Wno-stringop-overflow',
  '-Wno-stringop-truncation',
  '-Wno-maybe-uninitialized',
  '-Wno-ignored-qualifiers',
] + sdk_cflags

tier1_headers = include_directories('../public/tier1')
tier1_lib = static_library(
  'tier1',
  tier1_sources,
  c_args: tier1_cflags,
  cpp_args: tier1_cflags,
  dependencies: [ prebuilt_deps['tier0'] ],
  include_directories: [sdk_headers, tier1_headers],
)

tier1_dep = declare_dependency(
  compile_args: sdk_cflags,
  include_directories: tier1_headers,
  # tier1 headers require tier0
  dependencies: [ prebuilt_deps['tier0'] ],
  link_with: [ tier1_lib ],
)
