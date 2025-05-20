file(GLOB PJSIP_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjsip/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjsip/*.h
)
file(GLOB PJSIP-SIMPLE_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjsip-simple/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjsip-simple/*.h
)
file(GLOB PJSIP-UA_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjsip-ua/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjsip-ua/*.h
)
file(GLOB PJSUA-LIB_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjsua-lib/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjsua-lib/*.h
)

add_library(pjsip OBJECT
    ${PJSIP_SRC}
    ${PJSIP-SIMPLE_SRC}
    ${PJSIP-UA_SRC}
    ${PJSUA-LIB_SRC}
)
