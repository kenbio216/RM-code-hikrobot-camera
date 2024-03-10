#Cmake最小版本
CMAKE_MINIMUM_REQUIRED(VERSION 3.5)

SET(PROJECT_NAME Baldr)
project(${PROJECT_NAME})
SET(CMAKE_BUILD_TYPE RELEASE)
#SET(CMAKE_BUILD_TYPE DEBUG)
SET(CMAKE_CXX_STANDARD 11)

#可执行文件生成路径
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${PROJECT_SOURCE_DIR}/build)

#找到OpenCV包
FIND_PACKAGE(OpenCV REQUIRED)

#引用库
INCLUDE_DIRECTORIES(include)
INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIRS})
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include/eigen-3.3.7)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/Src)

#生成指定目标
FILE(GLOB_RECURSE SOURCE_FILES "${PROJECT_SOURCE_DIR}/Src/*.cpp")
ADD_EXECUTABLE(${PROJECT_NAME} Src/main.cpp ${SOURCE_FILES})

#将第三方的库链接到可执行文件
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${OpenCV_LIBS})
TARGET_LINK_LIBRARIES(${PROJECT_NAME} "/opt/DahuaTech/MVviewer/lib/libMVSDK.so")
TARGET_LINK_LIBRARIES(${PROJECT_NAME} "/opt/DahuaTech/MVviewer/module/USBDriver/libu3v-core.a")