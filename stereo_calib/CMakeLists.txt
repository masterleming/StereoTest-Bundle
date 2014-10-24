#stereo_calib
cmake_minimum_required (VERSION 2.6)
project (StereoCalib)
# The version number.
set (StereoCalib_VERSION_MAJOR 1)
set (StereoCalib_VERSION_MINOR 0)

set (OutputName stereo_calib)

# configure a header file to pass some of the CMake settings
# to the source code
#configure_file (
#  "${PROJECT_SOURCE_DIR}/StereoCalib_Config.h.in"
#  "${PROJECT_BINARY_DIR}/StereoCalib_Config.h"
#  )

# add the binary tree to the search path for include files
# so that we will find PointCloudConfig.h
include_directories("${PROJECT_BINARY_DIR}")
include_directories("${PROJECT_SOURCE_DIR}")

set( OpenCV_SOURCE_DIR "NOTFOUND" CACHE PATH "Path to OpenCV source root directory" )

if(EXISTS "${OpenCV_DIR}/samples/cpp/stereo_calib.cpp")
	set(calib_src "${OpenCV_DIR}/samples/cpp/stereo_calib.cpp" CACHE FILEPATH "Path to stereo_calib.cpp file." FORCE )
	set(OpenCV_SOURCE_DIR ${OpenCV_DIR} FORCE )
elseif(EXISTS "${OpenCV_SOURCE_DIR}/samples/cpp/stereo_calib.cpp")
	set(calib_src "${OpenCV_SOURCE_DIR}/samples/cpp/stereo_calib.cpp" CACHE FILEPATH "Path to stereo_calib.cpp file." FORCE )
else()
	set( calib_src "NOTFOUND" CACHE FILEPATH "Path to stereo_calib.cpp file." FORCE )
endif()

#stereo_calib
# add the executable
add_executable(${OutputName}
	${calib_src}
)

include_directories(${OpenCV_INCLUDE_DIRS})
target_link_libraries(${OutputName} ${OpenCV_LIBS})

# add the install targets
install (TARGETS ${OutputName} RUNTIME DESTINATION .)#${OutputName})
install(FILES conf/stereo_calib.xml DESTINATION .)#${OutputName})

# build a CPack driven installer package
#set(CPACK_PACKAGE_VERSION_MAJOR "${StereoCalib_VERSION_MAJOR}")
#set(CPACK_PACKAGE_VERSION_MINOR "${StereoCalib_VERSION_MINOR}")
#set(CPACK_GENERATOR "ZIP;TGZ")
#set(CPACK_SOURCE_GENERATOR "ZIP;TGZ")
#include(CPack)