cmake_minimum_required(VERSION 2.6 FATAL_ERROR)
project(sdf2sdf)
find_package(PCL 1.8 REQUIRED COMPONENTS common io visualization features)
find_package(OpenCV REQUIRED)
#zc:
message(STATUS "opencv-incdir: ${OpenCV_INCLUDE_DIRS}")
message(STATUS "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")
#to avoid "<incomplete type>" when debugging:
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_GLIBCXX_DEBUG")
message(STATUS "CMAKE_CXX_FLAGS_DEBUG: ${CMAKE_CXX_FLAGS_DEBUG}")

include_directories(${PCL_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
set(CMAKE_CXX_STANDARD 11)
set(SOURCE_FILES main.cpp PhiFuncGradients.cpp PhisFunc.cpp PhisFunc.h common.h selfCross.h selfCross.cpp PhiFuncGradients.h myPoint.h)
add_executable(sdf2sdf ${SOURCE_FILES})
target_link_libraries(sdf2sdf ${PCL_COMMON_LIBRARIES} ${PCL_IO_LIBRARIES} ${PCL_VISUALIZATION_LIBRARIES}
        ${PCL_FEATURES_LIBRARIES} ${OpenCV_LIBS})
