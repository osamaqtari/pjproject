include(FindPkgConfig)
include(FindPackageHandleStandardArgs)

find_package(PkgConfig)

pkg_check_modules(UUID uuid REQUIRED)
set(UUID_VERSION ${uuid_VERSION})

find_path(UUID_INCLUDE_DIR
  NAMES uuid.h
  HINTS ${UUID_ROOT} ${uuid_INCLUDEDIR} ${uuid_INCLUDE_DIRS}
  PATH_SUFFIXES include uuid
)

find_library(UUID_LIBRARY
  NAMES uuid
  HINTS ${UUID_ROOT} ${uuid_LIBDIR} ${uuid_LIBRARY_DIRS}
  PATH_SUFFIXES ${CMAKE_INSTALL_LIBDIR}
)

find_package_handle_standard_args(uuid
  REQUIRED_VARS UUID_LIBRARY UUID_INCLUDE_DIR
  VERSION_VAR UUID_VERSION
)

if (UUID_FOUND)
    mark_as_advanced(UUID_FOUND UUID_INCLUDE_DIR UUID_LIBRARY)
    if(PJSIP_STATIC_BUILD AND NOT ${UUID_STATIC_LIBRARY} STREQUAL "")
        add_library(uuid STATIC IMPORTED GLOBAL)
        set_target_properties(uuid PROPERTIES
            PROPERTY IMPORTED_LOCATION "${UUID_STATIC_LIBRARY}"
            INTERFACE_INCLUDE_DIRECTORIES "${UUID_INCLUDE_DIR}"
        )
    else()
        add_library(uuid SHARED IMPORTED GLOBAL)
        set_target_properties(uuid PROPERTIES
            IMPORTED_LOCATION "${UUID_LIBRARY}"
            INTERFACE_INCLUDE_DIRECTORIES "${UUID_INCLUDE_DIR}"
        )
    endif()
else()
    message(FATAL_ERROR "UUID library not found")
endif()

include_directories(${UUID_INCLUDE_DIRS})
if(TARGET_LINUX)
    add_definitions(-DHAVE_INTTYPES_H)
endif()
