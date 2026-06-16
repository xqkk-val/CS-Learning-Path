==实战 3 - 生成动态库并链接==

### 目标

把 `hello.cpp` 和 `world.cpp` 编译成**动态库**，然后让 `main.cpp` 链接它。

### 为什么学这个？

真实项目不会把所有文件都编译成一个可执行文件，而是：

- 公共功能 → 做成库（可以被多个程序复用）
  
- 主程序 → 链接这个库
  

---

### 步骤 1：重新组织文件结构

```
cd /home/xq/cmake_practice

# 创建 lib 目录存放库的源码
mkdir -p lib

# 把 hello 相关文件移到 lib 目录
mv hello.h hello.cpp lib/
# world.cpp 已经在 lib 目录? 如果没有就也移动一下
```

### 步骤 2：修改 CMakeLists.txt

```
cat > CMakeLists.txt << 'EOF'
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# 添加头文件搜索路径（因为 hello.h 现在在 lib 目录下）
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib)

# 生成动态库（SHARED）
add_library(mylib SHARED 
    lib/hello.cpp
    lib/world.cpp
)

# 生成可执行文件
add_executable(demo main.cpp)

# 链接动态库到可执行文件
target_link_libraries(demo mylib)
EOF
```

### 步骤 3：编译运行

bash

```
cd build
rm -rf *
cmake ..
make
./demo
```

---

### 预期输出

```
Hello from another file!
World function called!
```



同时你会发现 `build` 目录下多了一个 `libmylib.so`（Linux）文件——这就是生成的动态库。

------

### 关键命令解释

| 命令                                | 作用                           |
| :---------------------------------- | :----------------------------- |
| `include_directories(...)`          | 告诉编译器去哪里找 `.h` 头文件 |
| `add_library(mylib SHARED ...)`     | 生成动态库 `libmylib.so`       |
| `target_link_libraries(demo mylib)` | 把库链接到 `demo` 可执行文件   |

|      |      |
|---|---|
|      |      |
|      |      |
|      |      |

---

