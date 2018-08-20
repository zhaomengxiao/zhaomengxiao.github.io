---
title: c++ 調用MATLAB<engine>
date: 2018-03-22 10:44:23
tags:
- MATLAB
- C++
- tips
---
>初入C++，實在感受到了精通它的困難。用慣了方便好用的Matlab的plot指令，自然在苦於如何用C++畫些簡單的圖形來幫助自己驗證代碼的時候，想到了可不可以調用Matlab來畫圖。

其實是可以的，配置還非常方便，這裡我介紹一種調用MATLAB<engine>的方法：
## Quick Start
在C++中調用MATLAB<engine>，你會需要
<font color="#FF0000">头文件</font>，只需engine.h即可
```bash
engine.h
```
<font color="#FF0000">lib文件</font>，lib文件需要这三个：libmx.lib/libmat.lib/libeng.lib。

```bash
libmx.lib
libmat.lib
libeng.lib
```

## More info
>引擎相应的部分函数如下：
engOpen：启动Matlab引擎
engClose：关闭Matlab引擎
engGetArray：从Matlab引擎中获得一个Matlab矩阵，用于数据交换
engPutArray：从应用程序向Matlab引擎发送一个Matlab矩阵，用于数据交换
engEvalString：执行一个Matlab命令
engOutputBuffer：创建一个用于存储Matlab文本输出的字符缓冲区

## Example Code
```bash
#include "stdafx.h"
#include <iostream>
#include <math.h>
#include <string>
//#include <engine.h>

#include "engine.h"  
using namespace std;

void main()
{
	const int N = 50;
	double x[N], y[N];
	int j = 1;
	for (int i = 0; i<N; i++) //计算数组x和y  
	{
		x[i] = (i + 1);
		y[i] = sin(x[i]) + j * log(x[i]); //产生－之间的随机数赋给xx[i];  
		j *= -1;
	}

	Engine *ep = engOpen(""); //定义Matlab引擎指针。初始化  
	//ep=engOpen("");  
	if (!(ep)) //测试是否启动Matlab引擎成功。  
	{
		cout << "Can't start Matlab engine!" << endl;
		exit(1);
	}

	//定义mxArray，1行，N列的实数数组。然后将计算结果复制到创建的mx对象中，进入matlab engine计算。  
	mxArray *xx = mxCreateDoubleMatrix(1, N, mxREAL);
	mxArray *yy = mxCreateDoubleMatrix(1, N, mxREAL);

	//memcpy，从源src所指的内存地址的起始位置开始拷贝n个字节到目标dest所指的内存地址的起始位置中。数组赋值方法。  
	//mxGetPr返回数组指针：第一个元素指针  
	memcpy(mxGetPr(xx), x, N*sizeof(double)); //将数组x复制到mxarray数组xx中。  
	memcpy(mxGetPr(yy), y, N*sizeof(double)); //将数组x复制到mxarray数组yy中。  

	engPutVariable(ep, "xx", xx); //将mxArray数组xx写入到Matlab工作空间，命名为xx。  
	engPutVariable(ep, "yy", yy); //将mxArray数组yy写入到Matlab工作空间，命名为yy。  

	//向Matlab引擎发送画图命令。plot为Matlab的画图函数，参见Matlab相关文档。  
	engEvalString(ep, "plot(xx, yy); ");

	mxDestroyArray(xx); //销毁mxArray数组xx和yy。  
	mxDestroyArray(yy);

	cout << "Press any key to exit!" << endl;
	cin.get();
	engClose(ep); //关闭Matlab引擎。  
}

```
