add_library(
  tier1

  bitbuf.cpp
  newbitbuf.cpp
  byteswap.cpp
  characterset.cpp
  checksum_crc.cpp
  checksum_md5.cpp
  checksum_sha1.cpp
  commandbuffer.cpp
  convar.cpp
  datamanager.cpp
  diff.cpp
  generichash.cpp
  ilocalize.cpp
  interface.cpp
  KeyValues.cpp
  kvpacker.cpp
  lzmaDecoder.cpp
  # "lzss.cpp" [!$SOURCESDK]
  mempool.cpp
  memstack.cpp
  NetAdr.cpp
  splitstring.cpp
  # "processor_detect.cpp" [$WINDOWS||$X360]
  
  # [$POSIX]
  processor_detect_linux.cpp
  
  # [$LINUXALL||$PS3]
  qsort_s.cpp

  rangecheckedvar.cpp
  reliabletimer.cpp
  stringpool.cpp
  strtools.cpp
  strtools_unicode.cpp
  tier1.cpp
  tokenreader.cpp
  sparsematrix.cpp
  uniqueid.cpp
  utlbuffer.cpp
  utlbufferutil.cpp
  utlstring.cpp
  utlsymbol.cpp
  utlbinaryblock.cpp

  # [$LINUXALL]
  pathmatch.cpp

  snappy.cpp
  snappy-sinksource.cpp
  snappy-stubs-internal.cpp
)

target_compile_options(tier1 PUBLIC "${SDK_CFLAGS}")
target_compile_options(
  tier1 PRIVATE

  -Wno-pedantic
  -Wno-implicit-fallthrough
  -Wno-register
  -Wno-sign-compare
  -Wno-reorder
  -Wno-misleading-indentation
  -Wno-nonnull-compare
  -Wno-strict-aliasing
  -Wno-unused-function
  -Wno-unused-result
  -Wno-unused-value
  -Wno-volatile
  -Wno-class-memaccess
  -Wno-stringop-overflow
  -Wno-stringop-truncation
  -Wno-maybe-uninitialized
  -Wno-ignored-qualifiers
)

target_link_libraries(tier1 tier0)
target_include_directories(
  tier1 SYSTEM PUBLIC
  "${SDK_INCLUDES}"
  "${PROJECT_SOURCE_DIR}/public/tier1"
)

add_library(sdk::tier1 ALIAS tier1)
