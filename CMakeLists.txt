cmake_minimum_required(VERSION 3.14)
include(GNUInstallDirs)
project(TestApplicationProject VERSION 0.1.0)
find_package(PkgConfig REQUIRED)

#find Qt5 libraries with pkg-config
pkg_check_modules(QT5 REQUIRED Qt5Core Qt5Network Qt5Xml Qt5SerialPort Qt5XmlPatterns)

#our applicaiton
add_executable(TestApplication main.cpp CmdArgParser.h CmdArgParser.cpp)

#project options for Qt5
target_link_libraries(TestApplication ${QT5_LIBRARIES})
target_include_directories(TestApplication PUBLIC ${QT5_INCLUDE_DIRS})
target_compile_options(TestApplication PUBLIC ${QT5_CFLAGS_OTHER})
target_compile_options(TestApplication PUBLIC "-fPIC")

#project options for wl_iot_framework
target_include_directories(TestApplication PUBLIC
	"../wl_iot_framework/wliotproxy-src/libwliotproxy-base/include"
	"../wl_iot_framework/wliotproxy-src/libVDIL/include"
	"../wl_iot_framework/wliotproxy-src/libwliotproxy/include")
target_link_libraries(TestApplication "-lwliotproxy")
