cmake_minimum_required(VERSION 3.4.1)

#CMAKE_SOURCE_DIR 当前CMakeLists.txt所在目录
set(jnilibs "${CMAKE_SOURCE_DIR}/../jniLibs")

#头文件路径 Android在同步的时候会显示相关头文件
include_directories(
        util
        render
        sample
        glm
        inc
        inc/assimp
        inc/freetype_2_9_1
        model
        opencv_3_0_0
        egl
        looper
)

#GLOB操作  用一个变量表示正则表达式筛选的文件
file(GLOB src-files
        ${CMAKE_SOURCE_DIR}/*.cpp
        ${CMAKE_SOURCE_DIR}/render/*.cpp
        ${CMAKE_SOURCE_DIR}/util/*.cpp
        ${CMAKE_SOURCE_DIR}/sample/*.cpp
        ${CMAKE_SOURCE_DIR}/egl/*.cpp
        ${CMAKE_SOURCE_DIR}/looper/*.cpp)


#add_library指定构建原生库   Android Studio 还会在您同步项目后在 Project 视图中显示相关的头文件
add_library( # 设置库名字
             native-render

             # [STATIC | SHARED | MODULE] 设置库属性 静态 动态
             SHARED

             # 源码路径
             ${src-files}
        )


# 命令以找到 NDK 库并将其路径存储为一个变量
find_library( # 名字
              log-lib

              # 路径
              log )

#IMPORTED标志  导入构建好的动态库assimp
add_library(assimp SHARED IMPORTED )
#指定库路径
#set_target_properties(target1 target2 ...
#        PROPERTIES prop1 value1
#        prop2 value2 ...)

#ANDROID_ABI 添加库的多个 ABI 版本
set_target_properties(assimp PROPERTIES IMPORTED_LOCATION ${jnilibs}/${ANDROID_ABI}/libassimp.so)

add_library(opencv_java3 SHARED IMPORTED )
set_target_properties(opencv_java3 PROPERTIES IMPORTED_LOCATION ${jnilibs}/${ANDROID_ABI}/libopencv_java3.so)

add_library(freetype STATIC IMPORTED )
set_target_properties(freetype PROPERTIES IMPORTED_LOCATION ${jnilibs}/${ANDROID_ABI}/libfreetype.a)



#SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -fno-rtti -fno-exceptions")
#指定第三方庫
set(third-party-libs
        freetype
        assimp
        opencv_java3)

#预编译库链接现有的库
target_link_libraries( # 库名字 add_library定义
                       native-render

                       # 现有库名
                       ${log-lib}
                       ${third-party-libs}
                        #后面几个都是so库
                        #C:\Users\12774\AppData\Local\Android\Sdk\ndk\20.0.5594570\platforms\android-24\arch-arm\usr\lib
                       EGL
                       GLESv3
                       android
                       )

