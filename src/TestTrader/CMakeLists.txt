
#1. 确定CMake的最低版本需求
CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)

#2. 确定工程名
PROJECT(TestTrader LANGUAGES CXX)
SET(CMAKE_CXX_STANDARD 11)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/../build_${PLATFORM}/${CMAKE_BUILD_TYPE}/bin/TestTrader)

#7. 添加源码
file(GLOB SRCS *.cpp)

IF(MSVC)
	SET(LIBS WTSTools)
ELSE(GNUCCCC)
	SET(LIBS WTSTools dl)
ENDIF()

INCLUDE_DIRECTORIES(${INCS})
LINK_DIRECTORIES(${LNKS})

ADD_EXECUTABLE(TestTrader ${SRCS})
TARGET_LINK_LIBRARIES(TestTrader ${LIBS})

IF (MSVC)
ELSE (GNUCC)
	SET_TARGET_PROPERTIES(TestTrader PROPERTIES
        LINK_FLAGS_RELEASE -s)
ENDIF ()