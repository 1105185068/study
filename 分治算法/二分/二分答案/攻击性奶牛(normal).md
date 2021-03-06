# 攻击性奶牛(normal)
## 问题描述
Farmer John has built a new long barn, with N (2 <= N <= 100,000) stalls. The stalls are located along a straight line at positions x1,...,xN (0 <= xi <= 1,000,000,000). 

His C (2 <= C <= N) cows don't like this barn layout and become aggressive towards each other once put into a stall. To prevent the cows from hurting each other, FJ want to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. What is the largest minimum distance?

农民约翰建造了一个新的长牛棚，有N个牛棚(2<=N<=100,000)。牛棚位于x1，…，xN(0<=xi<=1,000,000,000,000,000)处的一条直线上。

他的C(2<=C<=N)奶牛不喜欢这样的牛棚布局，一旦被放到一个摊位上，就会变得咄咄逼人。为了防止母牛互相伤害，FJ想把牛分配到牛棚上，这样它们之间的最小距离就越大越好。最大最小距离是多少？

### 输入

+ 第1行：两个空格分隔的整数：n和C

+ 第2行.N+1：I+1行包含整数牛棚位置，xi
### 输出量

+ 第1行：一个整数：最大最小距离

### 样本输入
```
5 3
1
2
8
4
9
```
### 样本输出
```
3
```
### 暗示

产出详情：

FJ可以把他的3头牛放在第1、4和8位置的牛棚上，从而得到3头牛的最小距离。

输入数据量巨大，推荐扫描。

## 方法一：二分答案
**即测试```l```到```r```的```mid```方案是否可行**
+ **如果```mid```可行，则小于mid的都可行，则```l=mid+1```**
+ **如果```mid```不可行，则大于mid的都不可行，则```r=mid-1```**

## 代码示例
```c++
//二分答案 
#include <iostream>
#include <algorithm> 

using namespace std;


typedef long long ll;
const ll MAX=1e5+10;
ll a[MAX];
ll i,n,c,l,r,mid;


bool real(int x){
	int flag=a[1];
	int cnt=1;
	for(i=2;i<=n;i++){
		if(a[i]-flag>=x){
			flag=a[i];
			cnt++;
		}
		if(cnt>=c){
			return true;
		}
	}
	return false;
}


int main(int argc, char** argv) {
	cin>>n>>c;
	for(i=1;i<=n;i++){
		cin>>a[i];
	}
	sort(a+1,a+n+1);
	l=a[1];
	r=a[n];
	while(l<=r){
		mid=(l+r)>>1;
		if(real(mid)){
			l=mid+1;
		}
		else r=mid-1;
	}
	cout <<r;
	return 0;
}
```

**链接**<http://poj.org/problem?id=2456>
