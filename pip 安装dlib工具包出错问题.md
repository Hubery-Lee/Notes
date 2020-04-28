# ruby jekyll搭建Github Page

## 1.dlib的功能介绍

Dlib是一个现代化的C ++工具箱，其中包含用于在C ++中创建复杂软件以解决实际问题的机器学习算法和工具。它广泛应用于工业界和学术界，包括机器人，嵌入式设备，移动电话和大型高性能计算环境。Dlib的[开源许可证](https://www.dlib.net.cn/docs/license.html) 允许您在任何应用程序中免费使用它。

Dlib有很长的时间，包含很多模块，近几年作者主要关注在机器学习、深度学习、图像处理等模块的开发。

`想用dlib来做人脸识别`

## 2.安装中遇到的问题

**版本说明：**

- python3.7
- anaconda 5.3
- dlib 19.19
遇到的问题主要是import dlib 出错。

通过一天的往复折腾发现是我的cuda安装出现了错误。重新安装cuda后，编译通过。

## 3. 总结
[anaconda3-5.3.1+CUDA10.2+Cudnn6.0+pytorch1.4安装说明](https://blog.csdn.net/weixin_45953976/article/details/105547758)

**如何给conda配置国内源**

#配置常用库国内源，方便安装Numpy,Matplotlib等

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
```
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
```
#配置国内源，安装PyTorch用
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
```
#显示源地址（方便我们确认下载地址）

```
conda config --set show_channel_urls yes
```
安装常用库
```
pip install numpy matplotlib pillow pandas
```
**如何通过pycharm+anaconda配置python编程环境**

将pycharm的编译器配置成anacoda文件夹下的python.exe就可以了