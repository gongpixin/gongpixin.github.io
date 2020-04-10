---
layout: post
title: "hdu 4712 hamming distance(随机数法)"
categories:
tags:
---

Problem Description

(From wikipedia) For binary strings a and b the Hamming distance is equal to the number of ones in a XOR b.

For calculating Hamming distance between two strings a and b, they must have equal length.

Now given N different binary strings, please calculate the minimum Hamming distance between every pair of strings.

Input

The first line of the input is an integer T, the number of test cases.(0<T<=20)

Then T test case followed. The first line of each test case is an integer N (2<=N<=100000),

the number of different binary strings. Then N lines followed, each of the next N line is a string consist of five characters.

Each character is '0'-'9' or 'A'-'F', it represents the hexadecimal code of the binary string. For example,

the hexadecimal code "12345" represents binary string "00010010001101000101".

Output

For each test case, output the minimum Hamming distance between every pair of strings.

Sample Input

```
2
2 12345 54321
4 12345 6789A BCDEF 0137F
```

Sample Output

```
6
7
```

样例分析

```
12345 --> 0001 0010 0011 0100 0101
54321 --> 0101 0100 0011 0010 0001
          0100 0110 0000 0110 0100
6个1
```

code

```c++
#include <iostream>
#include <stdio.h>
#include <time.h>
#include <algorithm>
 
using namespace std;
 
const int LOOP_NUM = 400000;
 
char str[100000][6];
int num[100000];
     
int main() {
    srand((unsigned int)time(NULL));
    int T;
    int N;
     
    scanf("%d", &T);
    
    while (T--) {
        scanf("%d", &N);
         
        for (int i = 0; i < N; ++i) {
            scanf("%s", str[i]);
        }

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
         
        //这是一段看脸的代码
        int min_dis = 20;
        for (int i = 0; i < LOOP_NUM; ++i) {
            int fuck = rand() % N;
            int shit = rand() % N;
            if (fuck == shit) {
                continue;
            }
            int tmp = num[fuck] ^ num[shit];
            int sum = 0;
            while (tmp != 0) {
                sum += tmp & 1;
                tmp >>= 1;
            }
            min_dis = min(min_dis, sum);
        }
        printf("%d\n", min_dis);
    }
    
    return 0;
}
```
