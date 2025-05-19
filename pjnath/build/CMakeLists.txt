set(PJNATH_SRC
    ../src/pjnath/errno.c
    ../src/pjnath/ice_session.c
    ../src/pjnath/ice_strans.c
    ../src/pjnath/nat_detect.c
    ../src/pjnath/stun_auth.c
    ../src/pjnath/stun_msg.c
    ../src/pjnath/stun_msg_dump.c
    ../src/pjnath/stun_session.c
    ../src/pjnath/stun_sock.c
    ../src/pjnath/stun_transaction.c
    ../src/pjnath/turn_session.c
    ../src/pjnath/turn_sock.c
    ../src/pjnath/upnp.c
)

set(PJNATH_INC
    ../include/pjnath.h
    ../include/pjnath/config.h
    ../include/pjnath/errno.h
    ../include/pjnath/ice_session.h
    ../include/pjnath/ice_strans.h
    ../include/pjnath/nat_detect.h
    ../include/pjnath/stun_auth.h
    ../include/pjnath/stun_config.h
    ../include/pjnath/stun_msg.h
    ../include/pjnath/stun_session.h
    ../include/pjnath/stun_sock.h
    ../include/pjnath/stun_transaction.h
    ../include/pjnath/turn_session.h
    ../include/pjnath/turn_sock.h
    ../include/pjnath/types.h
    ../include/pjnath/upnp.h
)

add_library(pjnath OBJECT ${PJNATH_SRC} ${PJNATH_INC})
