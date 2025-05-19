set(PJNATH_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/errno.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/ice_session.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/ice_strans.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/nat_detect.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/stun_auth.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/stun_msg.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/stun_msg_dump.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/stun_session.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/stun_sock.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/stun_transaction.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/turn_session.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/turn_sock.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/pjnath/upnp.c
)

set(PJNATH_INC
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/config.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/errno.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/ice_session.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/ice_strans.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/nat_detect.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/stun_auth.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/stun_config.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/stun_msg.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/stun_session.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/stun_sock.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/stun_transaction.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/turn_session.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/turn_sock.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/types.h
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/pjnath/upnp.h
)

add_library(pjnath OBJECT ${PJNATH_SRC} ${PJNATH_INC})
