

#CMake指令

## 1>cmake_minimun_required:

指定CMake的最小版本支持,一般作为第一条cmake指令

#CMake版本支持指令-cmake

```cmake
#CMake设置最小版本支持版本为2.8
cmake_minimun_required(VERSION 2.8)
```





## 2>project:

定义工程的名称,并可以指定工程支持的语言

#CMake工程名称指令-cmake

```cmake
#指定工程的名称为HELLOWORLD
project(HELLOWORLD CXX)		#表示工程名为HELLOWORLD,使用的语言为c++
```



## 3>set:设置变量

#设置变量-cmake

```cmake
#定义变量SRC其值为sayhello.cpp hello.cpp
set(SRC sayhello.cpp hello.cpp)
```



## 4>add_executable:

通过依赖生成可执行程序
#编译生成可执行程序-cmake

```cmake
#编译main.cpp 生成main的可执行程序
add_executable(main mian.cpp)
```



## 5>include_directories:

向工程添加多个特定的头文件搜索路径,类似与g++编译指令中的-|
#头文件搜索-cmake

```cmake
#将/usr/lib/mylibfolder和./lib添加到工程路径中
include_directories(/usr/lib/mylibfolder ./lib)
```



## 6>link_directories:

向工程中添加多个特定的库文件搜索路径,类似于g++编译指令的-L选项
#库文件搜索-cmake


```cmake
#将/usr/lib/mylibfolder和./lib添加到库文件搜索路径中
link_directories(/usr/lib/mylibfolder ./lib)
```





## 7>add_library:

生成库文件(包括静态库和动态库)

#cmake生成库文件

```cmake
#通过SRC变量中的文件,生成动态库
add_library(hello SHARED ${SRC})	#该语句生成的是动态库
add_library(hello STATIC ${SRC})	#该语句生成的是静态率
库名+库的类型+依赖的文件
```



## 8> add_compile_options:

添加编译参数


```cmake
#添加编译参数	-wall -std=c++11
add_compile_options(-wall -std=c++11)
```

----------------------------------------------------------------------------

## 9>target_link_libraries:

为target目标文件添加需要链接的动态库,类似与g++编译中的-l指令

```cmake
#将hel1o动态库文件链接到可执行程序main中
target_link_libraries(main hello)
```



CMake常用变量

1>CMAKE_C_FLAGS:gcc编译选项的值

2>CMAKE_CXX_FLAGS:g++编译选项的值

```CMAKE
#在CMAKE_CXX_FLAGS编译选项后追加-std=c++11
Set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
```



3>CMAKE_BUILD_TYPE:编译类型(debug,release)

```cmake
#设定编译类型为Debug，调试时需要选择该模式
set(CMAKE_BUILD_TYPE Debug)
#设定编译类型为Release，发布需要选择该模式
set(CMAKE_BUILD_TYPE Release)
```

