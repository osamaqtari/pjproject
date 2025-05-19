set(PJMEDIA_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/alaw_ulaw.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/alaw_ulaw_table.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/audiodev.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/bidirectional.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/clock_thread.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/codec.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/conference.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/conf_switch.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/delaybuf.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/echo_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/echo_port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/echo_speex.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/echo_suppress.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/endpoint.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/errno.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/format.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/g711.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/jbuf.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/master_port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/mem_capture.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/mem_player.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/null_port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/plc_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/splitcomb.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/resample_resample.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/resample_libsamplerate.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/resample_port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/rtcp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/rtcp_xr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/rtp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/sdp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/sdp_cmp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/sdp_neg.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/session.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/silencedet.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/sound_legacy.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/sound_port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/stereo_port.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/stream.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/stream_info.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/stream_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/tonegen.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/transport_adapter_sample.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/transport_ice.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/transport_loop.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/transport_udp.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/types.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/wav_player.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/wav_playlist.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/wav_writer.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/wave.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/wsola.c
)

set(PJMEDIA-AUDIODEV_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-audiodev/audiodev.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-audiodev/errno.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-audiodev/legacy_dev.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-audiodev/null_dev.c
)

set(PJMEDIA-CODECS_SRC
  ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/audio_codecs.c
)

file(GLOB_RECURSE PJMEDIA_INC ${CMAKE_CURRENT_SOURCE_DIR}/../include/*.h)

if(WITH_SRTP)
    set(PJMEDIA_SRC ${PJMEDIA_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia/transport_srtp.c
    )
    include_directories(AFTER SYSTEM
        ${CMAKE_CURRENT_SOURCE_DIR}/../../third_party/srtp/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../../third_party/srtp/crypto/include
        ${CMAKE_CURRENT_SOURCE_DIR}/../../third_party/build/srtp
    )
endif()

if(WITH_PASSTHROUGH_CODECS)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/passthrough.c
    )
endif()

if(WITH_CODEC_GSM)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/gsm.c
    )
endif()

if(WITH_CODEC_OPUS)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/opus.c
    )
    include_directories(AFTER SYSTEM
       ${CMAKE_CURRENT_SOURCE_DIR}/../../third_party/opus/include
    )
endif()

if(WITH_CODEC_SPEEX)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/speex_codec.c
    )
    include_directories(AFTER SYSTEM
        ${CMAKE_CURRENT_SOURCE_DIR}/../../third_party/speex/include
    )
endif()

if(WITH_CODEC_ILBC)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/ilbc.c
    )
endif()

if(WITH_CODEC_IPP)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/ipp_codecs.c
    )
endif()

if(WITH_CODEC_L16)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/l16.c
    )
endif()

if(WITH_CODEC_G722)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/g722.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/g722/g722_dec.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/g722/g722_enc.c
    )
endif()

if(WITH_CODEC_G7221)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/g7221.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/g7221_sdp_match.c
    )
    include_directories(AFTER SYSTEM
        ${CMAKE_CURRENT_SOURCE_DIR}/../../third_party/g7221
    )
endif()

if(WITH_CODEC_AMRWB OR WITH_CODEC_AMRNB)
    set(PJMEDIA-CODECS_SRC ${PJMEDIA-CODECS_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/opencore_amr.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjmedia-codec/amr_sdp_match.c
    )
endif()

add_library(pjmedia OBJECT
    ${PJMEDIA_SRC}
    ${PJMEDIA_INC}
    ${PJMEDIA-AUDIODEV_SRC}
    ${PJMEDIA-CODECS_SRC}
)
