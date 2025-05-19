file(GLOB_RECURSE ILBC_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/*.h
    ${CMAKE_CURRENT_SOURCE_DIR}/config.h
)

set(ILBC_SRC ${ILBC_SRC}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/anaFilter.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/constants.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/createCB.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/doCPLC.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/enhancer.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/filter.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/FrameClassify.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/gainquant.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/getCBvec.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/helpfun.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/hpInput.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/hpOutput.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/iCBConstruct.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/iCBSearch.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/iLBC_decode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/iLBC_encode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/LPCdecode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/LPCencode.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/lsf.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/packing.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/StateConstructW.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/StateSearchW.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/syntFilter.c
)

include_directories(AFTER SYSTEM
    ${CMAKE_CURRENT_SOURCE_DIR}/.
    ${CMAKE_CURRENT_SOURCE_DIR}/../../ilbc/
)

add_library(ilbc OBJECT ${ILBC_SRC})
