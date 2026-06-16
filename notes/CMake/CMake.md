指令

1>cmake_minimun_required:指定CMake的最小版本支持,一般作为第一条cmake指令

```cmake
#CMake设置最小版本支持版本为2.8
cmake_minimun_required(VERSION 2.8)
```





2>project:定义工程的名称,并可以指定工程支持的语言

```cmake
#指定工程的名称为HELLOWORLD
project(HELLOWORLD CXX)		#表示工程名为HELLOWORLD,使用的语言为c++
```



3>set:显示变量

```cmake
#定义变量SRC其值为sayhello.cpp hello.cpp
set(SRC sayhello.cpp hello.cpp)
```



4>add_edecutable:通过依赖生成可执行程序

```cmake
#编译main.cpp 生成main的可执行程序
add_executbale(main mian.cpp)
```

