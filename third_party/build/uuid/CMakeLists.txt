include(FindPkgConfig)

pkg_check_modules(UUID uuid REQUIRED)

if(TARGET_LINUX)
    add_definitions(-DHAVE_INTTYPES_H)
endif()

include_directories(${UUID_INCLUDE_DIRS})
