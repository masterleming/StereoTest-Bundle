#TOP module
cmake_minimum_required (VERSION 2.6)
project (StereoTest-Bundle)
# The version number.
set (StereoTest-Bundle_VERSION_MAJOR 1)
set (StereoTest-Bundle_VERSION_MINOR 0)

#find_package(Boost REQUIRED COMPONENTS program_options)
find_package(OpenCV REQUIRED COMPONENTS core highgui imgproc features2d calib3d contrib gpu flann ml objdetect video)

add_subdirectory(picGrabber)
add_subdirectory(stereo_calib)
add_subdirectory(undistortedCam)

set(CMAKE_INSTALL_SYSTEM_RUNTIME_LIBS_SKIP TRUE)
include(InstallRequiredSystemLibraries)
install(PROGRAMS ${CMAKE_INSTALL_SYSTEM_RUNTIME_LIBS}
        DESTINATION .
)

include(CMakeExpandImportedTargets)
include(GetPrerequisites)

cmake_expand_imported_targets(expandedLibs LIBRARIES ${OpenCV_LIBS} ${CMAKE_BUILD_TYPE})
foreach(item ${expandedLibs})
	gp_append_unique(uniqueList ${item})
endforeach()

install(FILES ${uniqueList} DESTINATION . )
	
# build a CPack driven installer package
set(CPACK_PACKAGE_NAME "StereoTest-Bundle")
set(CPACK_PACKAGE_VENDOR "Krzysztof Pilch")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Stereovision tools bundle based on OpenCV.")
set(CPACK_PACKAGE_VERSION_MAJOR "${StereoTest-Bundle_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${StereoTest-Bundle_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION "${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "bundle")
set(CPACK_GENERATOR "ZIP;TGZ")
set(CPACK_SOURCE_GENERATOR "ZIP;TGZ")
set(CPACK_PACKAGE_DIRECTORY "cpack")
set(CPACK_COMPONENTS_ALL)
include(CPack)
