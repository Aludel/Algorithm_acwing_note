# 787. 归并排序

给定你一个长度为 $n$ 的整数数列。

请你使用归并排序对这个数列按照从小到大进行排序。

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
### 输出样例：
```text
1 2 3 4 5
```

## 模板步骤
1. 确定区域合法性
2. 确定分界点，选择中间点
3. 递归进行左右的排序
4. 使用temp数组进行归并
5. 合并其余项
6. 把temp数组的结果返回到arry数组上

## 细节
1. 归并排序不像快排，归并排序是稳定的，快排是不稳定排序（快排想变稳定，使用pair，连带下标进行排序）
2. 归并排序算法复杂度 $O(n.logn)$

## 模板
```c++
#include <iostream>
using namespace std;

const int N=100005;
int arry[N];
int temp[N];

void MergeSort(int q[],int lo,int hi) {
    //区域合法性判断
    if(lo>=hi) return ;
    
    // 分界点确定
    int mid=(lo+hi) >>1;
    // 进行递归排序
    MergeSort(q,lo,mid);
    MergeSort(q,mid+1,hi);
    // 排序完成，进行归并
    int k=0,i=lo,j=mid+1;
    while(i<=mid && j<=hi) {
        if(q[i]<=q[j]) {
            temp[k++]=q[i++];
        }
        else {
            temp[k++]=q[j++];
        }
    }
    // 合并其余项
    while(i<=mid) temp[k++]=q[i++];
    while(j<=hi) temp[k++]=q[j++];
    // 排序结果返回
    for(int i=lo,j=0;i<=hi;) {
        q[i++]=temp[j++];
    }
}
int main() {
    int n;
    cin>>n;
    for(int i=0;i<n;++i) {
        cin>>arry[i];
    }
    MergeSort(arry,0,n-1);
    
    for(int i=0;i<n;++i){
        cout<<arry[i]<<(i!=n ? " " : "");
    }
    cout<<endl;
    return 0;
}
```
