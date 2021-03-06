cmake_minimum_required(VERSION 3.5)
project(IFM3D_EXAMPLES)

set(CMAKE_MODULE_PATH
    ${IFM3D_EXAMPLES_SOURCE_DIR}/cmake/modules
    ${CMAKE_MODULE_PATH})

# force an out-of-source build of the code
include(MacroOutOfSourceBuild)
macro_ensure_out_of_source_build(
  "Please build ${PROJECT_NAME} out-of-source")

################################################
## Bring in dependent projects
################################################
find_package(ifm3d 0.9.0 CONFIG
  REQUIRED COMPONENTS camera framegrabber image pcicclient
  )

if(FORCE_OPENCV3)
  find_package(OpenCV 3 REQUIRED)
elseif(FORCE_OPENCV2)
  find_package(OpenCV 2.4 REQUIRED)
else()
  find_package(OpenCV REQUIRED)
endif()

################################################
## Build the examples
################################################
add_executable(ex-file_io ex-file_io.cpp)
target_link_libraries(ex-file_io
                      ifm3d::camera
                      ifm3d::framegrabber
                      ifm3d::image
                      ${OpenCV_LIBRARIES}
                      )

add_executable(ex-getmac ex-getmac.cpp)
target_link_libraries(ex-getmac ifm3d::camera)

add_executable(ex-fast_app_switch ex-fast_app_switch.cpp)
target_link_libraries(ex-fast_app_switch
                      ifm3d::camera
                      ifm3d::framegrabber
                      ifm3d::image
                      ifm3d::pcicclient
                      )

add_executable(ex-pcicclient_set_io ex-pcicclient_set_io.cpp)
target_link_libraries(ex-pcicclient_set_io
                      ifm3d::camera
                      ifm3d::pcicclient
                      )

add_executable(ex-pcicclient_async_messages ex-pcicclient_async_messages.cpp)
target_link_libraries(ex-pcicclient_async_messages
                      ifm3d::camera
                      ifm3d::pcicclient
                      )

add_executable(ex-timestamp ex-timestamp.cpp)
target_link_libraries(ex-timestamp
                      ifm3d::camera
                      ifm3d::framegrabber
                      ifm3d::image
                      )

add_executable(ex-exposure_times ex-exposure_times.cpp)
target_link_libraries(ex-exposure_times
                      ifm3d::camera
                      ifm3d::framegrabber
                      ifm3d::image
                      )
