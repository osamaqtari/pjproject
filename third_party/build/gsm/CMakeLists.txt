file(GLOB_RECURSE GSM_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/inc/*.h
    ${CMAKE_CURRENT_SOURCE_DIR}/config.h
)

set(GSM_SRC ${GSM_SRC}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/add.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/code.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/decode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_create.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_decode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_destroy.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_encode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_explode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_implode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/gsm_option.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/long_term.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/lpc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/preprocess.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/rpe.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/short_term.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/src/table.c
)

include_directories(AFTER SYSTEM
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../gsm/inc
)

add_definitions(-DSASR -DWAV49 -DNeedFunctionPrototypes=1)

add_library(gsm OBJECT ${GSM_SRC})
