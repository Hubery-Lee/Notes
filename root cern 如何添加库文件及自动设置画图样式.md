# root cern 如何添加库文件及自动设置画图样式

## 1.  rootlogon.C

```
//This is the file rootlogon.C
{
   printf("\nWelcome to the ROOT tutorials\n\n");
   printf("\nType \".x demos.C\" to get a toolbar from which to execute the demos\n");
   printf("\nType \".x demoshelp.C\" to see the help window\n\n");
   printf("==> Many tutorials use the file hsimple.root produced by hsimple.C\n");
   printf("==> It is recommended to execute hsimple.C before any other script\n\n");
}
```

### 1.1 如果想导入库函数，在rootlogon.C中添加

```
gSysteem->Load("xxx.so")
```

### 1.2 如果想设置默认画图样式，可以在rootlogon.C中设置

```C++
//This is the file rootlogon.C
{
    TStyle *myStyle = new TStyle("MyStyle","My Root Styles");

    //from ROOT	plain style
    myStyle->SetCanvasBorderMode(0);
    myStyle->SetPadBorderMode(0);
    myStyle->SetPadColor(0);
    myStyle->SetCanvasColor(0);
    myStyle->SetTitleColor(1);
    myStyle->SetStatColor(0);

    myStyle->SetLabelSize(0.03,"xyz");

    //default canvas positioning
    myStyle->SetCanvasDefX(900);
    myStyle->SetCanvasDefY(20);
    myStyle->SetCanvasDefH(550);
    myStyle->SetCanvasDefW(540);

    myStyle->SetPadBottomMargin(0.1);
    myStyle->SetPadTopMargin(0.1);
    myStyle->SetPadLeftMargin(0.1);
    myStyle->SetPadRightMargin(0.1);
    myStyle->SetPadTickX(1);//1表示图像右边画上坐标轴
    myStyle->SetPadTickY(1);//1表示图像上边画上坐标轴
    myStyle->SetFrameBorderMode(0);

    //Din letter
    myStyle->SetPaperSize(21,28);
    myStyle->SetOptStat(111111);//Show overflow and underflow
    myStyle->SetOptFit(1011); //这些参数什么意思
    myStyle->SetPalette(1);

    //apply the new style
    gROOT->SetStyle("MyStyle");//uncomment to set this style
    gROOT->ForceStyle();//use this style,not the one in root files
    
    printf("\n Beginning new ROOT session with private style\n");
}
```

![1570895640140](C:\Users\lee\OneDrive\Markdown_WorkSpace\软件测试笔记\images\1570895640140.png)

**注意** ：历史命令查看`cat ~/.root_hist` 

## 2. 将常用代码放到一个头文件中以提高效率

![1570896078958](C:\Users\lee\OneDrive\Markdown_WorkSpace\软件测试笔记\images\1570896078958.png)

![1570896177364](C:\Users\lee\OneDrive\Markdown_WorkSpace\软件测试笔记\images\1570896177364.png)

![1570896425100](C:\Users\lee\OneDrive\Markdown_WorkSpace\软件测试笔记\images\1570896425100.png)

![1570896447496](C:\Users\lee\OneDrive\Markdown_WorkSpace\软件测试笔记\images\1570896447496.png)