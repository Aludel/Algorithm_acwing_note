# 785. 快速排序

给定你一个长度为 $n$ 的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

## 输入格式

输入共两行，第一行包含整数 $n$。

第二行包含 $n$ 个整数（所有整数均在 $1 \sim 10^9$ 范围内），表示整个数列。

## 输出格式

输出共一行，包含 $n$ 个整数，表示排好序的数列。

## 数据范围

$1 \le n \le 100000$

### 输入样例：

```text
5
3 1 2 4 5
```

### 输出样例:
```text
1 2 3 4 5
```

## 快排Quick_Sort 递归表示基本步骤：
1. 确定区域合法性
2. 确定一个分界点x
3. 一次快排，使用双指针，若要实现从小到大排序，左指针 lo 应当跳过所有小于分界点 x 的数，最终停在大于等于 x 的数上；右指针 hi 应当跳过所有大于 x 的数，最终停在小于等于 x 的数上。，进行swap.
4. 进行递归快排
 
## 注意点
1. 确定什么时候可以进行swap操作 -> 在左边找到比x大的数，在右边找到比x小的数
2. 确定分界点如何进行选择，一般选择区域中间或者区域第一个数 -> Index = (lo+hi)>>1;
3. 双指针快排不同于单指针快排，双指针快排并不会使分界点经过一轮快排后处于正确位置
## 基本模板
```
#include <bits/stdc++.h>
using namespace std;

const int N=100005;
int arry[N];

void QuickSort(int q[], int lo, int hi) {
  // 先进行区域合法性判断
  if(lo>=hi) {return ;}

  // 这里的指针移动逻辑，考虑到了do-while里指针的移动逻辑(标准化)
  int i=lo-1;
  int j=hi+1;

  // 确定分界点（中间）
  int x=q[(lo+hi) >> 1];

  // 左右指针碰面的时候退出循环
  while(i<j) {
  do i++; while (q[i] > x);
  do j--; while (q[j] < x);
  // 两次do-while后，可能不满足i<j(非法),所以在进行swap的时候进行一次判断
  if(i<j) { swap( q[i], q[j]); }
  }
  
  // 继续进行递归快排
  // 如果使用i的话,这种写法，分界点不能为 lo，不然会有边界问题（eg: 1 2 then always 1 2 死循环）
  // QuickSort(q,lo,i-1);
  // QuickSort(q,i,hi);
  // 使用j的写法，不能使用hi作分界点，不然会有边界问题，死循环
  QuickSort(q,lo,j);
  QuickSort(q,j+1,hi);
}

int main() {
  int n;
  cin>>n;
  for(int i=0;i<n;++i) {
    cin>>arry[i];
  }
  QuickSort(arry,0,n-1);
  for(int i=0;i<n;++i) {
    cout<<arry[i]<<( i != n-1 ? " " : "");
  }
  return 0;
}
```
