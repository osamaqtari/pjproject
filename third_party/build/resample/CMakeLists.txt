set(RESAMPLE_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/src/largefilter.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/src/resample.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/src/resamplesubs.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/include/resamplesubs.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/src/smallfilter.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/src/stddefs.h
    ${CMAKE_CURRENT_SOURCE_DIR}/config.h
)

include_directories(BEFORE SYSTEM
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../resample/include
)

add_library(resample OBJECT ${RESAMPLE_SRC})
