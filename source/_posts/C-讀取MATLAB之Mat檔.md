---
title: C++ 讀取MATLAB之Mat檔
date: 2018-03-22 17:54:59
tags:
- tips
- cpp
- MATLAB
---
```bash
#include "stdafx.h"
#include <iostream>
#include <math.h>
#include <string>
#include <Eigen\Dense>
#include "engine.h" 
#include <mat.h>
using namespace Eigen;
using namespace std;
int main()
{
	int len = 10000;
	MATFile * pMatFile;
	mxArray * pMxArray1;
	mxArray * pMxArray2;
	double * pData1;
	double * pData2;
	pMatFile = matOpen("test_mat_file.mat", "w");
	if (!pMatFile) return -1;
	pMxArray1 = mxCreateDoubleMatrix(len, 1, mxREAL);
	pMxArray2 = mxCreateDoubleMatrix(len, 1, mxREAL);
	if (!pMxArray1) return -1;
	pData1 = (double *)mxCalloc(len, sizeof(double));
	pData2 = (double *)mxCalloc(len, sizeof(double));
	if (!pData1 || !pData2) return -1;
	for (int i = 0; i < len; i++)
	{
		pData1[i] = (double)i / 10000.0;
		pData2[i] = sin(2.0 * 3.14159 * pData1[i]);
	}
	mxSetData(pMxArray1, pData1);
	mxSetData(pMxArray2, pData2);
	matPutVariable(pMatFile, "time", pMxArray1);
	matPutVariable(pMatFile, "wave", pMxArray2);
	mxFree(pData1);
	mxFree(pData2);
	matClose(pMatFile);
	
	return 0;
}
```