## 2. 升级 CMakeLists.txt（使用变量）


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

## 4. 对比：不用变量 vs 用变量

| 方式     | CMakeLists.txt 写法                                          |
| :------- | :----------------------------------------------------------- |
| 不用变量 | `add_executable(demo main.cpp hello.cpp world.cpp ...)`      |
| 用变量   | `set(SOURCES main.cpp hello.cpp world.cpp ...)` `add_executable(demo ${SOURCES})` |

**好处**：如果新增文件（如 `world.cpp`），只需要改 `set` 那一行，不需要改 `add_executable`。

------

## 5. 验证你理解了

尝试修改：**再创建一个 `world.cpp`，在 main 中调用它的函数**，然后在 `set(SOURCES ...)` 里加上 `world.cpp`。

能独立完成吗？完成了把 `cmake ..` 和 `make` 的输出发给我。

------

## 记住这个模式

cmake

```
# 定义变量
set(变量名 值1 值2 值3)

# 使用变量
${变量名}
```



**常用变量名习惯**：

- `SOURCES` / `SRC`：源文件列表
- `HEADERS`：头文件列表
- `EXECUTABLE_NAME`：可执行程序名称