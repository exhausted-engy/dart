# Search all header and source files
file(GLOB hdrs "*.hpp")
file(GLOB srcs "*.cpp")

set(dart_collision_hdrs ${dart_collision_hdrs} ${hdrs} PARENT_SCOPE)
set(dart_collision_srcs ${dart_collision_srcs} ${srcs} PARENT_SCOPE)

# Generate header for this namespace
dart_get_filename_components(header_names "collision_fcl headers" ${hdrs})
dart_generate_include_header_list(
  collision_fcl_headers
  "dart/collision/fcl/"
  "collision_fcl headers"
  ${header_names}
)
configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/fcl.hpp.in
  ${CMAKE_CURRENT_BINARY_DIR}/fcl.hpp
)

# Install
install(
  FILES ${hdrs} ${CMAKE_CURRENT_BINARY_DIR}/fcl.hpp
  DESTINATION include/dart/collision/fcl
  COMPONENT headers
)
