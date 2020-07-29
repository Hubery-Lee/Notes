# 💘VSCODE IDE在C/C++项目编程中的使用

## 🌴IDE的作用

IDE的作用就是有用户交互界面的代码调试编辑器（也称集成开发环境，Integrated Development Environment）

### 💨c/c++编程主要基于两类编译器

- gcc, `开源、更新较快`
- visual studio,`微软全家桶`

所有linux系统的均是用gcc，linux系统对c/c++的支持更好。linux系统的核心代码基本是用c/c++编写的。

windows系统上c/c++编程一般用`visual studio`,当然，为了用到与linux上一样的开源gcc编译器，可以在windows上安装`mingw`或者`cywin`两种中的任意一款编译器。

### 🛴gcc编译器的没有图形Debug界面

visual studio自带的调试界面，编程比较方便。gcc的调试需要用`gdb`,而gdb存在的缺陷是其没有采用命令行调试，需要记住的命令太多，但缺少图像界面，大大降低了编程人员的生成效率。

由于gdb自身没有合适的IDE,项目配置通常用`makefile`。makefile继承linux系统下万物用命令行解决的风格。为了避免编写令人难懂的makefile文件，程序员开发了用于生成makefile的`cmake`工具 .

gcc等属于开源社区的软件，特点是版本多，没有统一的标准。导致很多公司开发了各自的IDE，如，JetBrain 公司的`Cion`, 微软公司的`VSCode`和IBM公司的`eclipse`等。VSCode,Cion和Eclipse均是top5的c/c++编辑器。其中，VSCode是后起之秀，由微软2015年发布的快平台编辑器。网上介绍较多，再此不再细说，感兴趣的同志可以自己去百度或谷歌一下。下面将介绍VSCode的C++代码调试。

## 🚀VSCode

VSCode是一款IDE编辑器，注意是`编辑器`说白了就跟`记事本`一样，只是它额外具备配置编译环境和调试代码的功能。就跟notepat++很像。项目的编译环境配置文件通常由两个组成`task.json`和`launch.json`。

- task.json `负责配置生成可执行文件`
- launch.json `负责调试`

具体VSCode的使用文件可以参考[官方说明文档](https://code.visualstudio.com/docs)
下面分别从单文件调试和项目文件调试两个方面进行测试，具体测试文档可参看[我的哔哩哔哩视频](https://www.bilibili.com/video/BV1TK4y187kn)

### 🚲单文件，单步调试

- 配置生成可执行文件task.json

- 配置调试执行文件lauch.json

```task.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "C/C++: cpp.exe build active file",
            "command": "D:\\Qt\\Tools\\mingw730_64\\bin\\cpp.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "D:\\Qt\\Tools\\mingw730_64\\bin"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build"
        }
    ]
}
```
```lauch.json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++.exe - 生成和调试活动文件",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\Qt\\Tools\\mingw730_64\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "g++.exe build active file"
        }
    ]
}
```

### 🚍项目文件，单步调试

- CMake `负责配置生成可执行文件`
- launch.json `负责调试`
```CMakeLists.txt

cmake_minimum_required(VERSION 3.10.0)
# 定义项目名称变量PROJECT_NAME, 默认值为demo
set(PROJECT_NAME demo)

set(CMAKE_BUILD_TYPE "Debug")

set(CMAKE_CXX_STANDARD_REQUIRED 14)
#----------------------------------------------------------------------------
# Setup include directory for this project
#

include_directories(${PROJECT_SOURCE_DIR}/include)
#----------------------------------------------------------------------------
# Locate sources and headers for this project
# NB: headers are included so they will show up in IDEs
#
file(GLOB sources ${PROJECT_SOURCE_DIR}/src/*.cc)
file(GLOB headers ${PROJECT_SOURCE_DIR}/include/*.h)

# 指定生成目标
add_executable(${PROJECT_NAME} main.cc ${sources} ${headers})

```
```launch.json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}\\build\\demo.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\Qt\\Tools\\mingw730_64\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```
