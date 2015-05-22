cmake_minimum_required(VERSION 2.4.6)

PROJECT(ORB_SLAM)

IF(NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE Release)
ENDIF()

MESSAGE("Build type: " ${CMAKE_BUILD_TYPE})

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -Wall  -O3 -march=native ")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall  -O3 -march=native")

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

LIST(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules)

find_package(OpenCV REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(Cholmod REQUIRED)
find_package(Boost COMPONENTS thread REQUIRED)

include_directories(
${PROJECT_SOURCE_DIR}/include
${PROJECT_SOURCE_DIR}
${EIGEN3_INCLUDE_DIR}
${CHOLMOD_INCLUDE_DIR}
${Boost_INCLUDE_DIRS}
)

#add_library(${PROJECT_NAME} SHARED
add_executable(${PROJECT_NAME}
src/Tracking.cc
src/LocalMapping.cc
src/LoopClosing.cc
src/ORBextractor.cc
src/ORBmatcher.cc
src/FramePublisher.cc
src/Converter.cc
src/MapPoint.cc
src/KeyFrame.cc
src/Map.cc
src/MapPublisher.cc
src/Optimizer.cc
src/PnPsolver.cc
src/Frame.cc
src/KeyFrameDatabase.cc
src/Sim3Solver.cc
src/Initializer.cc
src/main.cc
)

target_link_libraries(${PROJECT_NAME}
${OpenCV_LIBS}
${EIGEN3_LIBS}
${Boost_LIBRARIES}
cholmod
boost_system
${PROJECT_SOURCE_DIR}/Thirdparty/DBoW2/lib/libDBoW2.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_core.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_solver_cholmod.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_solver_dense.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_stuff.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_types_sba.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_types_sim3.so
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/lib/libg2o_types_slam3d.so
)

