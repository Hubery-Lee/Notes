# 🌌利用VSCode调试Geant4项目和Qt项目

==**注意**==

- VSCode只是一个具有用户交互界面、可设置断点调试的集成开发环境，并具有编辑器的一些特色功能，如：代码补全、格式自动化和语法自动检查等。直白的理解，他是一个具有很多集成功能的高端编辑器，属于前端，代码的编译链接执行需要交给其他一些软件，如CMake等。

- Geant4和Qt均是基于c++语言，调试程序需要用gdb。那么，调试geant4和Qt程序与调试C++程序一样没有什么区别。


## 🧭c++如何开启调试模式
C++单文件编译
```
g++ main.cpp -o a.out
```
C++单文件gdb调试
```
g++ -g main.cpp -o a.out
gdb a.out
```
## 🚀geant4 和qt等项目文件如何用调试
C++项目的链接通常采用可采用CMake，需要编写`CMakeLists.txt`
如需打开调试模式，只需奖`CMAKE_BUILD_TYPE` 设置成`"Debug"`模式即可。
```
set(CMAKE_BUILD_TYPE "Debug")
```


