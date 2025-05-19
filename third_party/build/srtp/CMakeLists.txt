set(SRTP_SRC
    # cihers
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/cipher.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/null_cipher.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/cipher_test_cases.c

    # hashes
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/null_auth.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/auth.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/auth_test_cases.c

    # replay
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/replay/rdb.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/replay/rdbx.c

    # math
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/math/datatypes.c

    # kernel
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/kernel/crypto_kernel.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/kernel/alloc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/kernel/key.c

    # srtpobj
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/srtp/srtp.c

    # errors
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/pjlib/srtp_err.c
)

file(GLOB_RECURSE SRTP_INC
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/include/*.h
    ${CMAKE_CURRENT_SOURCE_DIR}/config.h
)

include_directories(BEFORE SYSTEM
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp
)
add_definitions(-DHAVE_CONFIG_H)

add_library(srtp OBJECT ${SRTP_SRC} ${SRTP_INC})
