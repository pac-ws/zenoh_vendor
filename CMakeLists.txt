cmake_minimum_required(VERSION 3.10)
project(zenoh_vendor)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)

set(ZENOH_arch_new zenoh-plugin-ros2dds-1.1.1-aarch64-unknown-linux-gnu-standalone.zip)
set(ZENOH_new zenoh-plugin-ros2dds-1.1.1-x86_64-unknown-linux-gnu-standalone.zip)

if($ENV{ROS_NAMESPACE} MATCHES "^r[0-9]+$")
  # arm64 linux
  set(ZENOH_ZIP_FILE ${ZENOH_arch_new})
  
else()
  # x86_64 desktop
  set(ZENOH_ZIP_FILE ${ZENOH_new})

endif()

add_custom_command(
  OUTPUT
  ${CMAKE_CURRENT_BINARY_DIR}/zenoh-bridge-ros2dds
  COMMAND unzip -o ${CMAKE_CURRENT_SOURCE_DIR}/vendor_binaries/${ZENOH_ZIP_FILE} -d ${CMAKE_CURRENT_BINARY_DIR}
  DEPENDS
  ${CMAKE_CURRENT_SOURCE_DIR}/vendor_binaries/${ZENOH_ZIP_FILE}
)

add_custom_target(
  build_zenoh ALL
  DEPENDS
  ${CMAKE_CURRENT_BINARY_DIR}/zenoh-bridge-ros2dds
)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/zenoh-bridge-ros2dds 
  PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ GROUP_EXECUTE WORLD_EXECUTE
  DESTINATION bin)

set(MY_EXECUTABLE "${CMAKE_CURRENT_BINARY_DIR}/zenoh-bridge-ros2dds")

install(
    PROGRAMS ${MY_EXECUTABLE}
    DESTINATION lib/${PROJECT_NAME}
)

ament_package()
