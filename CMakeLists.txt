cmake_minimum_required(VERSION 3.28)

project(pjproject)

################################################################################
# build options
################################################################################

# miscs
set(CMAKE_VERBOSE_MAKEFILE ON)

# build type
set(PJSIP_STATIC_BUILD          OFF CACHE BOOL "enable static build")

# features
set(WITH_SRTP                   ON  CACHE BOOL "enable SRTP")
set(WITH_SSL                    ON  CACHE BOOL "enable SSL")
set(WITH_RESAMPLE_LIBRESAMPLE   OFF CACHE BOOL "enable libresample ressampling")
set(WITH_UUID_LIB               ON  CACHE BOOL "enable libUUID")

set(WITH_PASSTHROUGH_CODECS     OFF CACHE BOOL "enable passthrough codecs")
set(WITH_CODEC_SPEEX            OFF CACHE BOOL "enable speex codec")
set(WITH_CODEC_ILBC             OFF CACHE BOOL "enable ilbc codec")
set(WITH_CODEC_IPP              OFF CACHE BOOL "enable ipp codecs")
set(WITH_CODEC_GSM              ON  CACHE BOOL "enable gsm codec")
set(WITH_CODEC_G711             ON  CACHE BOOL "enable g711 codec")
set(WITH_CODEC_G722             ON  CACHE BOOL "enable g722 codec")
set(WITH_CODEC_G7221            OFF CACHE BOOL "enable g7221 codec")
set(WITH_CODEC_L16              ON  CACHE BOOL "enable l16 codec")
set(WITH_CODEC_AMRNB            OFF CACHE BOOL "enable amr narrowband codec")
set(WITH_CODEC_AMRWB            OFF CACHE BOOL "enable amr wideband codec")
set(WITH_CODEC_OPUS             OFF CACHE BOOL "enable opus codec")

set(WITH_AEC_SPEEX              OFF CACHE BOOL "enable speex aec")

# auto-fix incompatibles options
if(NOT WITH_CODEC_SPEEX AND WITH_AEC_SPEEX)
    set(WITH_AEC_SPEEX OFF)
    message(WARNING "disabling WITH_AEC_SPEEX because WITH_CODEC_SPEEX is OFF...")
endif()

if(WITH_CODEC_AMRWB OR WITH_CODEC_AMRNB)
    if(WITH_CODEC_IPP)
        set(WITH_CODEC_IPP OFF)
        message(WARNING "disabling WITH_CODEC_IPP because WITH_CODEC_AMRWB or WITH_CODEC_AMRNB is ON...")
    endif()
    if(WITH_PASSTHROUGH_CODECS)
        set(WITH_PASSTHROUGH_CODECS OFF)
        message(WARNING "disabling WITH_PASSTHROUGH_CODECS because WITH_CODEC_AMRWB or WITH_CODEC_AMRNB is ON...")
    endif()
endif()

if(WITH_CODEC_G7221 AND WITH_CODEC_IPP)
    set(WITH_CODEC_G7221 OFF)
    message(WARNING "disabling WITH_CODEC_G7221 because WITH_CODEC_IPP is ON...")
endif()


################################################################################
# Features specific
################################################################################

set(CODEC_LIBS)

if(WITH_SRTP)
    add_definitions(-DPJMEDIA_HAS_SRTP=1)
else()
    add_definitions(-DPJMEDIA_HAS_SRTP=0)
endif()

if(WITH_SSL)
    add_definitions(-DPJ_HAS_SSL_SOCK=1)
else()
    add_definitions(-DPJ_HAS_SSL_SOCK=0)
endif()

if(WITH_AUDIODEV_PORTAUDIO)
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_PORTAUDIO=1)
else()
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_PORTAUDIO=0)
endif()

if(WITH_AUDIODEV_COREAUDIO)
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_COREAUDIO=1)
else()
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_COREAUDIO=0)
endif()

if(WITH_AUDIODEV_OPENSL)
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_OPENSL=1)
else()
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_OPENSL=0)
endif()

if(WITH_AUDIODEV_WMME)
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_WMME=1)
else()
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_WMME=0)
endif()

if(WITH_AUDIODEV_ALSA)
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_ALSA=1)
    set(AUDIODEV_LIBS ${AUDIODEV_LIBS} asound)
else()
    add_definitions(-DPJMEDIA_AUDIO_DEV_HAS_ALSA=0)
endif()

if(WITH_RESAMPLE_LIBRESAMPLE)
    add_definitions(-DPJMEDIA_RESAMPLE_IMP=PJMEDIA_RESAMPLE_LIBRESAMPLE)
    set(RESAMPLING_NAME "resample")
elseif(WITH_RESAMPLE_LIBSAMPLERATE)
    add_definitions(-DPJMEDIA_RESAMPLE_IMP=PJMEDIA_RESAMPLE_LIBSAMPLERATE)
    set(RESAMPLING_NAME "libsamplerate")
else()
    add_definitions(-DPJMEDIA_RESAMPLE_IMP=PJMEDIA_RESAMPLE_NONE)
    set(RESAMPLING_NAME "none")
endif()

if(WITH_PASSTHROUGH_CODECS)
    add_definitions(-DPJMEDIA_HAS_PASSTHROUGH_CODECS=1)
else()
    add_definitions(-DPJMEDIA_HAS_PASSTHROUGH_CODECS=0)
endif()

if(WITH_CODEC_SPEEX)
    add_definitions(-DPJMEDIA_HAS_SPEEX_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_SPEEX_CODEC=0)
endif()

if(WITH_CODEC_ILBC)
    add_definitions(-DPJMEDIA_HAS_ILBC_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_ILBC_CODEC=0)
endif()

if(WITH_CODEC_IPP)
    add_definitions(-DPJMEDIA_HAS_INTEL_IPP=1)
else()
    add_definitions(-DPJMEDIA_HAS_INTEL_IPP=0)
endif()

if(WITH_CODEC_GSM)
    add_definitions(-DPJMEDIA_HAS_GSM_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_GSM_CODEC=0)
endif()

if(WITH_CODEC_G722)
    add_definitions(-DPJMEDIA_HAS_G722_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_G722_CODEC=0)
endif()

if(WITH_CODEC_G7221)
    add_definitions(-DPJMEDIA_HAS_G7221_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_G7221_CODEC=0)
endif()

if(WITH_CODEC_L16)
    add_definitions(-DPJMEDIA_HAS_L16_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_L16_CODEC=0)
endif()

if(WITH_AEC_SPEEX)
    add_definitions(-DPJMEDIA_HAS_SPEEX_AEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_SPEEX_AEC=0)
endif()

if(WITH_CODEC_AMRNB)
    add_definitions(-DPJMEDIA_HAS_OPENCORE_AMRNB_CODEC=1)
    set(CODEC_LIBS ${CODEC_LIBS} opencore-amrnb)
else()
    add_definitions(-DPJMEDIA_HAS_OPENCORE_AMRNB_CODEC=0)
endif()

if(WITH_CODEC_AMRWB)
    add_definitions(-DPJMEDIA_HAS_OPENCORE_AMRWB_CODEC=1)
    set(CODEC_LIBS ${CODEC_LIBS} opencore-amrwb)
else()
    add_definitions(-DPJMEDIA_HAS_OPENCORE_AMRWB_CODEC=0)
endif()

if(WITH_CODEC_OPUS)
    add_definitions(-DPJMEDIA_HAS_OPUS_CODEC=1)
else()
    add_definitions(-DPJMEDIA_HAS_OPUS_CODEC=0)
endif()


################################################################################
# Hardware specific
################################################################################
if(WITH_FLOATING_POINT)
    add_definitions(-DPJ_HAS_FLOATING_POINT=1)
else()
    add_definitions(-DPJ_HAS_FLOATING_POINT=0)
endif()


################################################################################
# OS specific
################################################################################

# Linux
if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    add_definitions(
        -DPJ_LINUX=1
        -DPJ_SOCK_HAS_GETADDRINFO=1
        -DPJ_SOCK_HAS_INET_ATON=1
        -DPJ_SOCK_HAS_INET_PTON=1
        -DPJ_SOCK_HAS_INET_NTOP=1
    )
    set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} -fPIC)
    set(OS_LIBS rt m pthread)
    if(WITH_SSL)
        set(OS_LIBS ${OS_LIBS} ssl crypto)
    endif()
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    add_definitions(
        -DPJ_DARWINOS=1
        -DPJ_HAS_SEMAPHORE_H=1
        -DPJ_SOCK_HAS_INET_ATON=1
        -DPJ_SOCK_HAS_INET_PTON=1
        -DPJ_SOCK_HAS_INET_NTOP=1
    )
    set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} -fPIC)
    set(OS_LIBS)
    if(WITH_SSL)
        set(OS_LIBS ${OS_LIBS} ssl crypto)
    endif()
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    add_definitions(-DPJ_WIN32=1)
    set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS})
    set(OS_LIBS)
else()
    message(FATAL_ERROR "Unsupported platform: ${CMAKE_SYSTEM_NAME}")
endif()

################################################################################
# Print summary
################################################################################
message("Target OS:       ${CMAKE_SYSTEM_NAME}")
message("Options:")
message("- SRTP:          ${WITH_SRTP}")
message("- SSL:           ${WITH_SSL}")
message("- Speex AEC:     ${WITH_AEC_SPEEX}")
message("Codecs:")
message("- passthrough:   ${WITH_PASSTHROUGH_CODECS}")
message("- speex:         ${WITH_CODEC_SPEEX}")
message("- gsm:           ${WITH_CODEC_GSM}")
message("- ilbc:          ${WITH_CODEC_ILBC}")
message("- intel ipp:     ${WITH_CODEC_IPP}")
message("- g722:          ${WITH_CODEC_G722}")
message("- g7221:         ${WITH_CODEC_G7221}")
message("- l16:           ${WITH_CODEC_L16}")
message("- amr narrowband:${WITH_CODEC_AMRNB}")
message("- amr wideband:  ${WITH_CODEC_AMRWB}")
message("- opus:          ${WITH_CODEC_OPUS}")
message("Resampling:      ${RESAMPLING_NAME}")
message("Audio dev libs:  ${AUDIODEV_LIBS}")


################################################################################
# Common
################################################################################

# sub-directories
set(PJSIP_SUBDIRECTORIES pjlib pjlib-util pjnath pjmedia pjsip)

foreach(SUBDIRECTORY ${PJSIP_SUBDIRECTORIES})
    set(PJSIP_INCLUDES ${PJSIP_INCLUDES} ${SUBDIRECTORY}/include/)
endforeach()
include_directories(${CMAKE_FIND_ROOT_PATH}/usr/include})
include_directories(AFTER SYSTEM . ${PJSIP_INCLUDES} ${CMAKE_BINARY_DIR})

add_subdirectory(third_party/build)
foreach(SUBDIRECTORY ${PJSIP_SUBDIRECTORIES})
    add_subdirectory(${SUBDIRECTORY}/build)
    set(TARGET_OBJECTS_LIST
        ${TARGET_OBJECTS_LIST}
        $<TARGET_OBJECTS:${SUBDIRECTORY}>
    )
endforeach()

# build target
if(NOT PJSIP_STATIC_BUILD)
    add_library(
        ${PROJECT_NAME} SHARED
        ${TARGET_OBJECTS_LIST} ${THIRDPARTY_OBJECTS_LIST}
    )
else()
    add_library(
        ${PROJECT_NAME} STATIC
        ${TARGET_OBJECTS_LIST} ${THIRDPARTY_OBJECTS_LIST}
    )
endif()

target_link_libraries(${PROJECT_NAME}
    ${OS_LIBS}
    ${CODEC_LIBS}
    ${AUDIODEV_LIBS}
    ${THIRDPARTY_LIBRARIES_LIST}
)

target_include_directories(${PROJECT_NAME} INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/pjlib/include
    ${CMAKE_CURRENT_SOURCE_DIR}/pjlib-util/include
    ${CMAKE_CURRENT_SOURCE_DIR}/pjsip/include
    ${CMAKE_CURRENT_SOURCE_DIR}/pjmedia/include
)
