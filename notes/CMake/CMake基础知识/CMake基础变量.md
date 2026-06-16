CMake常用变量
#CMake基础变量

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




