cmake_minimum_required(VERSION 2.8.3)
project(wy_localization)

set( catkin_package_DEPENDENCIES
)
find_package(catkin REQUIRED COMPONENTS ${catkin_package_DEPENDENCIES} )
find_package(PCL 1.2 REQUIRED)

find_package( catkin REQUIRED
    COMPONENTS
    roscpp
    message_generation
    std_msgs
    genmsg
    geometry_msgs
    sensor_msgs			
)

add_message_files( DIRECTORY msg
    FILES
)

generate_messages( 
    DEPENDENCIES 
    std_msgs
    geometry_msgs
    sensor_msgs	
)

catkin_package(
    INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/include
    LIBRARIES ${PROJECT_NAME}
    CATKIN_DEPENDS ${catkin_package_DEPENDENCIES}
    message_runtime
    std_msgs
    geometry_msgs
    sensor_msgs	
    roscpp
    DEPENDS Eigen
)
set( CMAKE_CXX_FLAGS "-std=c++11 -O3" )

include_directories(
    ${catkin_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
#    ${G2O_INCLUDE_DIRS}
#    ${CSPARSE_INCLUDE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)



add_subdirectory(wy_localization_lib)
set (EXTRA_LIBS ${EXTRA_LIBS} wy_localization_lib)

include_directories(/home/pc/catkin_ws/devel/lib)
link_directories(/home/pc/catkin_ws/devel/lib)
add_executable(pose_visualization ${CMAKE_CURRENT_SOURCE_DIR}/src/pose_visualization.cpp)
target_link_libraries(pose_visualization ${catkin_LIBRARIES} libwy_localization_lib.so)

#install( TARGETS ${PROJECT_NAME}
 #   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
 #   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
 #   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
#)

#add_dependencies( ${PROJECT_NAME} ${catkin_EXPORTED_TARGETS} )

include_directories(/home/pc/catkin_ws/devel/lib)
link_directories(/home/pc/catkin_ws/devel/lib)
add_executable(pose_provider ${CMAKE_CURRENT_SOURCE_DIR}/src/pose_provider.cpp)
target_link_libraries(pose_provider ${catkin_LIBRARIES} libwy_localization_lib.so)

include_directories(/home/pc/catkin_ws/devel/lib)
link_directories(/home/pc/catkin_ws/devel/lib)
add_executable(pose_fusion_provider ${CMAKE_CURRENT_SOURCE_DIR}/src/pose_fusion_provider.cpp)
target_link_libraries(pose_fusion_provider ${catkin_LIBRARIES} libwy_localization_lib.so)

include_directories(/home/pc/catkin_ws/devel/lib)
link_directories(/home/pc/catkin_ws/devel/lib)
add_executable(FFT_temp ${CMAKE_CURRENT_SOURCE_DIR}/src/FFT_temp.cpp)
target_link_libraries(FFT_temp ${catkin_LIBRARIES} libwy_localization_lib.so)

include_directories(/home/pc/catkin_ws/devel/lib)
link_directories(/home/pc/catkin_ws/devel/lib)
add_executable(KL_temp ${CMAKE_CURRENT_SOURCE_DIR}/src/KL_temp.cpp)
target_link_libraries(KL_temp ${catkin_LIBRARIES} libwy_localization_lib.so)

