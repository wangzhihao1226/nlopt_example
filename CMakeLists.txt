cmake_minimum_required(VERSION 3.15)
project(prc_nlopt)

include(D:/library/vcpkg/scripts/buildsystems/vcpkg.cmake)  ## add vcpkg path

set(CMAKE_CXX_STANDARD 14)

find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})
include_directories(include)

find_package(NLOPT REQUIRED)
include_directories(${NLOPT_INCLUDE_DIRS})

add_executable(example src/main.cpp include/nmpc/nmpc_controller.h include/nmpc/obstacle.h)

target_link_libraries(example PRIVATE ${NLOPT_INCLUDE_DIRS}/../lib/nlopt.lib)

add_executable(example2 src/sqp_example.cpp)
target_compile_definitions(example2 PRIVATE _USE_MATH_DEFINES)
target_link_libraries(example2 PRIVATE ${NLOPT_INCLUDE_DIRS}/../lib/nlopt.lib)

add_executable(vector_example src/vector_example.cpp)
target_compile_definitions(vector_example PRIVATE _USE_MATH_DEFINES)
target_link_libraries(vector_example PRIVATE ${NLOPT_INCLUDE_DIRS}/../lib/nlopt.lib)

add_executable(nmpc src/nmpc/nmpc_main.cpp src/nmpc/nmpc_controller.cpp src/nmpc/vehicle_model.cpp src/nmpc/nmpc_utils.cpp src/nmpc/reference_trajectory_generator.cpp src/nmpc/obstacle.cpp)
target_compile_definitions(nmpc PRIVATE _USE_MATH_DEFINES)
target_link_libraries(nmpc PRIVATE ${NLOPT_INCLUDE_DIRS}/../lib/nlopt.lib)