# 问题描述
给你***N***行***4***列的数，从每一列选一个数，问使他们的和为***0***的情况有多少种 （***N<=4000***）
## 解题思路
**将4列数字二分为两列两列数字，对每两列数字各自求和，将所求的所有和保存在```p[]```,```q[]```两个数组中，如果```p[]+q[]=0```，即找到满足题目的一种情况,然后对数组```p[]```和数组```q[]```使用双指针进行查找。这种方法会比直接双重循环遍历快一些**
**这时要注意一个问题，对于7,7和-7，-7，算4种情况**
+ 即如果p[]的前后两个元素相同，需要将p[]指向7然后不动，移动right，使其计数完后归为原位，再让下一个同样的7计数。
+ 此处也可以记录下第一个7所匹配的-7的数目，然后如果p[]的下一个也是7，则让其ans直接加上相同的数目。

## 代码示例
```c++
#include <iostream>
#include <bits/stdc++.h>

using namespace std;

const int MAX=4e3+10;
int a[MAX],b[MAX],c[MAX],d[MAX];
int p[MAX*MAX],q[MAX*MAX];


int main(int argc, char** argv) {
	int i,j,n;
	int ans=0;
	int cnt=0;
	cin>>n;
	for(i=0;i<n;i++){
		cin>>a[i]>>b[i]>>c[i]>>d[i];
	}
	for(i=0;i<n;i++){
		for(j=0;j<n;j++){
			p[cnt]=a[i]+b[j];
			q[cnt]=c[i]+d[j];
			cnt++; 
		}
	}
	//对两个数组进行升序排序
	sort(p,p+cnt);
	sort(q,q+cnt);
	
	/*直接双重循环遍历找所有满足的情况 
	for(i=0;i<n*n;i++){
		for(j=0;j<n*n;j++){
			if (p[i]+q[j]==0){
			ans++;
			}
		}
	}
	*/
	
	//接下来双指针，对其中第一个从尾开始遍历，另一个(即第二个)从头部开始遍历
	
	int left=cnt-1,right=0;
	while(left>=0&&right<=cnt-1){
	
	if(p[left]+q[right]==0){
		//记录在第二行满足与第一行和为0的所有数的始末位置，用start和end记录 
		int start=right;
		while(q[right]==q[right+1]){
		right++;
			}
		int end=right;
		
		ans=ans+end-start+1;
		
		//如果p的下一个与其相同，则在访问p的下一个之前将right归位到原始位置，再访问下一个p 
		if(p[left]==p[left-1]){
			right=start;
			left--;
			}
		//如果不相同则直接访问下一个p 的值 
		else left--;	
		}

	else if(p[left]+q[right]>0){
		left--;
	}
	
	else right++;
	} 

	cout<<ans;
	
	return 0;
}
```

**链接**<http://121.36.44.188/problem/1120>
