set(PJLIB_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/activesock.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/addr_resolv_sock.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/array.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/config.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/errno.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/except.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/guid.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/hash.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/ip_helper_generic.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/list.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/lock.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/log.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/ioqueue_select.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_info.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_time_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_timestamp_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/pool.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/pool_buf.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/pool_caching.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/pool_policy_malloc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/rand.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_qos_common.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/string.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/timer.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/types.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_select.c
)

set(PJLIB_INC
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/activesock.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/addr_resolv.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/array.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/assert.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/config.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/config_site.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/config_site_sample.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/errno.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/file_access.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/file_io.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/ip_helper.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/lock.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/log.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/os.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/pool.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/sock.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/sock_select.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/string.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/types.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/compat/errno.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/compat/socket.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/compat/stdarg.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/compat/string.h
)

if(WITH_SSL)
    set(PJLIB_SRC ${PJLIB_SRC}
    ../src/pj/ssl_sock_common.c
    ../src/pj/ssl_sock_dump.c
    ../src/pj/ssl_sock_ossl.c)
endif()

if(WITH_BUILTIN_OPENSSL)
    include_directories(BEFORE SYSTEM
    ../../third_party
    ../../third_party/openssl
 ${CMAKE_CURRENT_BINARY_DIR}/../../third_party/build/openssl
 ${CMAKE_CURRENT_BINARY_DIR}/../../third_party/build/openssl/openssl/crypto)
endif()

if(WITH_UUID_LIB)
    include_directories(AFTER SYSTEM ../../third_party/uuid)
    add_definitions(-DHAVE_UUID_LIB=1)
    set(PJLIB_SRC ${PJLIB_SRC} ../src/pj/guid_uuid.c)
else()
    set(PJLIB_SRC ${PJLIB_SRC} ../src/pj/guid_simple.c)
endif()

if(TARGET_LINUX OR TARGET_MACOSX)
    set(PJLIB_SRC ${PJLIB_SRC}
    ../src/pj/addr_resolv_sock.c
    ../src/pj/file_access_unistd.c
    ../src/pj/file_io_ansi.c
    ../src/pj/ioqueue_select.c
    ../src/pj/log_writer_stdout.c
    ../src/pj/os_core_unix.c
    ../src/pj/os_error_unix.c
    ../src/pj/os_time_unix.c
    ../src/pj/os_timestamp_posix.c
    ../src/pj/sock_bsd.c
    ../src/pj/sock_qos_bsd.c)

    if(TARGET_LINUX)
        set(PJLIB_INC ${PJLIB_INC} ../include/pj/compat/os_linux.h)
    elseif(TARGET_MACOSX)
        set(PJLIB_INC ${PJLIB_INC} ../include/pj/compat/os_darwinos.h)
    endif()
endif()

if(TARGET_WINDOWS)
    set(PJLIB_SRC ${PJLIB_SRC}
    ../src/pj/addr_resolv_sock.c
    ../src/pj/file_access_win32.c
    ../src/pj/file_io_win32.c
    ../src/pj/log_writer_stdout.c
    ../src/pj/os_core_win32.c
    ../src/pj/os_error_win32.c
    ../src/pj/os_time_win32.c
    ../src/pj/os_timestamp_win32.c
    ../src/pj/sock_bsd.c
    ../src/pj/sock_qos_bsd.c)
endif()

add_library(pjlib OBJECT ${PJLIB_SRC} ${PJLIB_INC})
