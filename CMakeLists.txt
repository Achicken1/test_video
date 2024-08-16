cmake_minimum_required(VERSION 3.10)
project(tcp_video_stream)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 查找OpenCV库
find_package(OpenCV REQUIRED)

# 查找FFmpeg库
find_package(PkgConfig REQUIRED)
pkg_check_modules(AVFORMAT REQUIRED libavformat)
pkg_check_modules(AVCODEC REQUIRED libavcodec)
pkg_check_modules(AVUTIL REQUIRED libavutil)
pkg_check_modules(SWSCALE REQUIRED libswscale)

# 可执行文件及其源代码
add_executable(tcp_video_stream video.cpp)

# 链接OpenCV和FFmpeg库
target_link_libraries(tcp_video_stream ${OpenCV_LIBS} 
                       ${AVFORMAT_LIBRARIES} 
                       ${AVCODEC_LIBRARIES} 
                       ${AVUTIL_LIBRARIES} 
                       ${SWSCALE_LIBRARIES})

# 包含FFmpeg头文件路径
target_include_directories(tcp_video_stream PRIVATE 
                           ${AVFORMAT_INCLUDE_DIRS} 
                           ${AVCODEC_INCLUDE_DIRS} 
                           ${AVUTIL_INCLUDE_DIRS} 
                           ${SWSCALE_INCLUDE_DIRS})
