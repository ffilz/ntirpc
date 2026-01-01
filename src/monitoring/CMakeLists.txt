########### next target ###############

set(CMAKE_CXX_STANDARD 17)

SET(ntirpcmonitoring_SRCS
  monitoring.cc
)

add_library(ntirpcmonitoring SHARED ${ntirpcmonitoring_SRCS})
add_sanitizers(ntirpcmonitoring)
set_target_properties(ntirpcmonitoring PROPERTIES
  VERSION ${NTIRPC_VERSION}
  SOVERSION "${NTIRPC_MAJOR_VERSION}${NTIRPC_MINOR_VERSION}"
  )
target_include_directories(ntirpcmonitoring     PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/prometheus-cpp-lite/core/include)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pedantic-errors -Werror -Wall -Wextra")
install(TARGETS ntirpcmonitoring DESTINATION ${CMAKE_INSTALL_LIBDIR})

########### install files ###############
install(FILES  include/monitoring.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/ntirpc)
