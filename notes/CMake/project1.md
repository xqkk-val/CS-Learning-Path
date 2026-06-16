## 你的第一个实战（现在就做，5分钟）

在 VSCode 中：

**Step 1**：新建 `CMakeLists.txt`

cmake

```
cmake_minimum_required(VERSION 3.10)
project(FirstDemo)

add_executable(demo main.cpp)
```



**Step 2**：新建 `main.cpp`

cpp

```
#include <iostream>
int main() {
    std::cout << "CMake on VM works!" << std::endl;
    return 0;
}
```



**Step 3**：在 VSCode 终端执行

bash

```
mkdir build && cd build
cmake ..
make
./demo
```



**Step 4**：看到输出 `CMake on VM works!` —— 环境验证完成











## 实战目标2

掌握 `set` 定义变量，让 CMakeLists.txt 更简洁、易维护。

------

## 1. 创建多文件项目

在 `/home/xq/cmake_practice/` 下创建以下文件：

### 创建 `hello.h`

bash

```
cat > hello.h << 'EOF'
#ifndef HELLO_H
#define HELLO_H

void sayHello();

#endif
EOF
```



### 创建 `hello.cpp`

bash

```
cat > hello.cpp << 'EOF'
#include <iostream>
#include "hello.h"

void sayHello() {
    std::cout << "Hello from another file!" << std::endl;
}
EOF
```



### 修改 `main.cpp`

bash

```
cat > main.cpp << 'EOF'
#include "hello.h"

int main() {
    sayHello();
    return 0;
}
EOF
```



------

## 2. 升级 CMakeLists.txt（使用变量）

bash

```
cat > CMakeLists.txt << 'EOF'
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# 使用 set 定义变量，把所有源文件放在一起
set(SOURCES
    main.cpp
    hello.cpp
)

# 使用变量 ${SOURCES} 代替手写所有文件名
add_executable(demo ${SOURCES})
EOF
```



------

## 3. 编译运行

bash

```
cd build
rm -rf *   # 清空旧的编译产物
cmake ..
make
./demo
```



**预期输出**：

text

```
Hello from another file!
```