include(CheckLibraryExists)

set(SRTP_SRC
    # cihers
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/cipher.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/null_cipher.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/cipher_test_cases.c

    # hashes
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/null_auth.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/auth.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/auth_test_cases.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/sha1.c

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

include_directories(BEFORE SYSTEM
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/include/
    ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp
)

CHECK_LIBRARY_EXISTS(crypto EVP_aes_128_gcm "" SSL_HAS_AES_GCM)

if (SSL_HAS_AES_GCM)
    set(SRTP_SRC ${SRTP_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/aes_icm_ossl.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/aes_gcm_ossl.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/hash/hmac_ossl.c
    )
    add_definitions(-DOPENSSL -DGCM)
else()
    set(SRTP_SRC ${SRTP_SRC}
        ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/aes.c
        ${CMAKE_CURRENT_SOURCE_DIR}/../../srtp/crypto/cipher/aes_icm.c
    )
endif()

add_definitions(-DHAVE_CONFIG_H)
add_library(srtp OBJECT ${SRTP_SRC})
