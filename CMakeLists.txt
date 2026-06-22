# Sources
include(cmake/sources.cmake)

# Target
if(CLIENTCOMMON_COMPILE_SOURCES)
    add_library(clientcommon
        ${CLIENTCOMMON_SOURCES}
    )
    set(CLIENTCOMMON_TARGET_SCOPE PUBLIC)
else()
    add_library(clientcommon INTERFACE)
    set(CLIENTCOMMON_TARGET_SCOPE INTERFACE)
endif()

target_compile_features(clientcommon ${CLIENTCOMMON_TARGET_SCOPE} cxx_std_17)

# Angle Includes
include(cmake/include.cmake)

target_include_directories(clientcommon
    ${CLIENTCOMMON_TARGET_SCOPE}
        ${CLIENTCOMMON_INCLUDE}
)

# DevKit Usage
if(CLIENTCOMMON_COMPILE_SOURCES AND COMMAND devkit_finalize)
    devkit_finalize(clientcommon)
endif()

# Tests
if(UNITER_BUILD_TESTS)
    include(cmake/test.cmake)
endif()




