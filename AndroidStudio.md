https://developer.android.google.cn/studio/projects/add-native-code

AS编译nativeC++代码

https://developer.android.google.cn/training/articles/perf-jni

jni入门

你进一个网站要清楚这个网站内容的排布 看清哪一部分才是你想要的

mmp智商不够用了啊艹



Android Studio

```
Android Studio 会将 Gradle 用作构建系统的基础
项目的依赖项在 build.gradle 文件中按名称指定。Gradle 可以自动查找您的依赖项，并在 build 中提供这些依赖项。
您可以在 build.gradle 文件中声明模块依赖项、远程二进制依赖项以及本地二进制依赖项。

Android Studio 提供了几种不同类型的模块（模块是源文件和编译设置的集合）：
库模块：
Android库 -> 产物为AAR文件（包含源代码 资源 清单）
Java库 -> 产物JAR文件（Java源代码）

Android支持CMake或者ndk-build配合gradle构建C/C++代码库（联调原生代码库 也就是so文件）

NDK： 一个工具集，让您能够在 Android 项目中使用 C 和 C++ 代码；它提供了各种平台库，让您能够管理原生 Activity 并访问实体设备组件，例如传感器和轻触输入
```



静态库 动态库区别（代码变成程序中  链接的过程不同 导致代码被载入的过程不同）

https://www.cnblogs.com/codingmengmeng/p/6046481.html

```
静态库在程序编译时会被连接到目标代码中，程序运行时将不再需要该静态库，因此体积较大。

动态库在程序编译时并不会被连接到目标代码中，而是在程序运行是才被载入，因此在程序运行时还需要动态库存在，因此代码体积较小。（适合多个程序共用 多进程共享资源）
```

