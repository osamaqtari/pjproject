file(GLOB_RECURSE SPEEX_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/*.h
    ${CMAKE_CURRENT_SOURCE_DIR}/config.h
)

set(SPEEX_SRC ${SPEEX_SRC}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/bits.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/buffer.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/cb_search.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/exc_10_16_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/exc_10_32_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/exc_20_32_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/exc_5_256_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/exc_5_64_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/exc_8_128_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/fftwrap.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/filterbank.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/filters.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/gain_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/gain_table_lbr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/hexc_10_32_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/hexc_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/high_lsp_tables.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/jitter.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/kiss_fft.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/kiss_fftr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/lpc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/lsp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/lsp_tables_nb.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/ltp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/mdf.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/modes.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/modes_wb.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/nb_celp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/preprocess.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/quant_lsp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/resample.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/sb_celp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/scal.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/smallft.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/speex.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/speex_callbacks.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/speex_header.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/stereo.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/vbr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/vorbis_psy.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/vq.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/libspeex/window.c
)

include_directories(AFTER SYSTEM
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../speex/include
)

add_definitions(-DHAVE_CONFIG_H -D_USE_MATH_DEFINES)

add_library(speex OBJECT ${SPEEX_SRC})
