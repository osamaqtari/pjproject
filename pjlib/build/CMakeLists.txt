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
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/ssl_sock_common.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/ssl_sock_dump.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/ssl_sock_ossl.c
    )
endif()

if(WITH_UUID_LIB)
    add_definitions(-DHAVE_UUID_LIB=1)
    set(PJLIB_SRC ${PJLIB_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/guid_uuid.c
    )
else()
    set(PJLIB_SRC ${PJLIB_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/guid_simple.c
    )
endif()

if(UNIX)
    set(PJLIB_SRC ${PJLIB_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/addr_resolv_sock.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/file_access_unistd.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/file_io_ansi.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/ioqueue_select.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/log_writer_stdout.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_core_unix.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_error_unix.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_time_unix.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_timestamp_posix.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_bsd.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_qos_bsd.c
    )

    if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
        set(PJLIB_INC ${PJLIB_INC}
            ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/compat/os_linux.h
        )
    elseif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
        set(PJLIB_INC ${PJLIB_INC}
            ${CMAKE_CURRENT_SOURCE_DIR}/../include/pj/compat/os_darwinos.h
        )
    endif()
elseif(WIN32)
    set(PJLIB_SRC ${PJLIB_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/addr_resolv_sock.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/file_access_win32.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/file_io_win32.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/log_writer_stdout.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_core_win32.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_error_win32.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_time_win32.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/os_timestamp_win32.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_bsd.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../src/pj/sock_qos_bsd.c
    )
endif()

add_library(pjlib OBJECT ${PJLIB_SRC} ${PJLIB_INC})
