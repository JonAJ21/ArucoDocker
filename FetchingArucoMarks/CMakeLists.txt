cmake_minimum_required(VERSION 3.10)

project(
    FetchingArucoMarks
    CXX
)

# Подключение дополнительных библиотек. Если собираете у себя -- указывайте свои пути.
# include_directories("C:/Program Files (x86)/vcpkg/installed/x64-windows/include")
# link_directories("C:/Program Files (x86)/vcpkg/installed/x64-windows/lib")
# set(CMAKE_PREFIX_PATH "C:/Program Files (x86)/vcpkg/installed/x64-windows/share")


include_directories("include")

find_package(cppzmq REQUIRED)
find_package(OpenCV CONFIG REQUIRED)

if(NOT ${ZeroMQ_FOUND})
    message("ZeroMQ not found!")
endif()


add_executable(main "main.cpp")
target_link_libraries(main ${OpenCV_LIBS} cppzmq)