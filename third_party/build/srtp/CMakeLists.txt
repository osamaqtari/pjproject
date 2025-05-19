set(SRTP_SRC
    # cihers
    ../../srtp/crypto/cipher/cipher.c
    ../../srtp/crypto/cipher/null_cipher.c
    ../../srtp/crypto/cipher/cipher_test_cases.c

    # hashes
    ../../srtp/crypto/hash/null_auth.c
    ../../srtp/crypto/hash/auth.c
    ../../srtp/crypto/hash/auth_test_cases.c

    # replay
    ../../srtp/crypto/replay/rdb.c
    ../../srtp/crypto/replay/rdbx.c

    # math
    ../../srtp/crypto/math/datatypes.c

    # kernel
    ../../srtp/crypto/kernel/crypto_kernel.c
    ../../srtp/crypto/kernel/alloc.c
    ../../srtp/crypto/kernel/key.c

    # srtpobj
    ../../srtp/srtp/srtp.c

    # errors
    ../../srtp/pjlib/srtp_err.c
)

file(GLOB_RECURSE SRTP_INC ../../srtp/include/*.h config.h)

include_directories(BEFORE SYSTEM
    .
    ../../srtp/include/
    ../../srtp/crypto/include/
    ../../srtp
)
add_definitions(-DHAVE_CONFIG_H)

add_library(srtp OBJECT ${SRTP_SRC} ${SRTP_INC})
