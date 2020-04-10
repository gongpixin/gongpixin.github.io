---
layout: post
title: "hdu 4712 hamming distance(随机数法)"
categories:
tags:
---
 
## Problem Description

(From wikipedia) For binary strings a and b the Hamming distance is equal to the number of ones in a XOR b.
For calculating Hamming distance between two strings a and b, they must have equal length.
Now given N different binary strings, please calculate the minimum Hamming distance between every pair of strings.
 

## Input

The first line of the input is an integer T, the number of test cases.(0<T<=20)
Then T test case followed. The first line of each test case is an integer N (2<=N<=100000),
the number of different binary strings. Then N lines followed, each of the next N line is a string consist of five characters.
Each character is '0'-'9' or 'A'-'F', it represents the hexadecimal code of the binary string. For example,
the hexadecimal code "12345" represents binary string "00010010001101000101".
 

## Output

For each test case, output the minimum Hamming distance between every pair of strings.
 

## Sample Input

```
2
2 12345 54321
4 12345 6789A BCDEF 0137F
```


## Sample Output

```
6
7
```


## 样例分析

```
12345 --> 0001 0010 0011 0100 0101
54321 --> 0101 0100 0011 0010 0001
          0100 0110 0000 0110 0100
6个'1'
```


## 代码

``` c++
#include <iostream>
#include <stdio.h>
#include <time.h>
#include <algorithm>
 
using namespace std;
 
const int LOOP_NUM = 400000;
 
char str[100005][8]; //16进制数
int num[100005]; //10进制数
     
int main()
{
    srand((unsigned int)time(NULL));
    int T; //测试用例个数
    int N; //每个测试用例中二进制数的个数
     
        scanf("%d", &T);
     
        while (T--) {
            scanf("%d", &N);
             
                for (int i = 0; i < N; ++i) {
                    scanf("%s", str[i]);
                }
            //转为10进制
            for (int i = 0; i < N; ++i) {
                int tmp = 0;
                for (int j = 0; j < 5; ++j) {
                    if ('0' <= str[i][j] && str[i][j] <= '9') {
                        tmp = (tmp << 4) + (str[i][j] - '0');
                    } else {
                        tmp = (tmp << 4) + (str[i][j] - 'A') + 10;
                    }
                }
                num[i] = tmp;
            }
             
                //随机选一部分求...看脸
                int minDis = 21;
            for (int i = 0; i < LOOP_NUM; ++i) {
                int fuck = rand() % N; //
                int shit = rand() % N;
                if (fuck == shit) {
                    continue;
                }
                //异或
                int tmp = num[fuck] ^ num[shit];
                //统计'1'的个数
                int sum = 0;
                while (tmp != 0) {
                    sum += tmp & 1;
                    tmp >>= 1;
                }
                //更新最小值
                minDis = min(minDis, sum);
            }
            printf("%d\n", minDis);
        }
     
        //system("pause");
        return 0;
}
```
