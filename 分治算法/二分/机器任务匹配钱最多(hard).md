# 机器任务匹配钱最多(hard)
## 问题描述(English)
Today the company has m tasks to complete. The ith task need xi minutes to complete. Meanwhile, this task has a difficulty level yi. The machine whose level below this task’s level yi cannot complete this task. If the company completes this task, they will get (500*xi+2*yi) dollars.

The company has n machines. Each machine has a maximum working time and a level. If the time for the task is more than the maximum working time of the machine, the machine can not complete this task. Each machine can only complete a task one day. Each task can only be completed by one machine.

The company hopes to maximize the number of the tasks which they can complete today. If there are multiple solutions, they hopes to make the money maximum.

### Input

The input contains several test cases. 

The first line contains two integers N and M. N is the number of the machines.M is the number of tasks(1 < =N <= 100000,1<=M<=100000).

The following N lines each contains two integers xi(0<xi<1440),yi(0=<yi<=100).xi is the maximum time the machine can work.yi is the level of the machine.

The following M lines each contains two integers xi(0<xi<1440),yi(0=<yi<=100).xi is the time we need to complete the task.yi is the level of the task.

### Output

For each test case, output two integers, the maximum number of the tasks which the company can complete today and the money they will get.

### Sample Input
```
1 2
100 3
100 2
100 1
```
### Sample Output
```
1 50004
```

## 问题描述(Chinese)

**给你N个机器和M个任务， 每个任务有两个值花费时间x和难度y, 每个机器也有两个值最大工作时间x1和最大工作难度y1， 机器可以胜任某个工作的条件是x1>=x && y1>=y,机器胜任一个工作可以拿到500*x+2*y的钱，现在问你怎么匹配才能使匹配数最大且钱数最多**
+ Xi<= 1440 yi<=100
+ 1 < =N <= 100000,1<=M<=100000

## 二分
### 解题思路
**对任务先x后y降序排序，对机器以x为主降序排序，让机器匹配机器的y恰好大于等于任务的y，这样才能使匹配结果钱数最大化**

**链接**<http://acm.hdu.edu.cn/showproblem.php?pid=4864>

### 代码示例
```c++
//压轴题500*x+2*y的任务机器

#include<bits/stdc++.h>
using namespace std;

typedef long long ll;

const ll MAXN =  1e5+10;

struct mach{
    ll x,y;

    //结构体重载运算符，说明两个mach结构体互相比较的实质是比较其成员变量x， 并且成员变量x越大的mach结构体越大
    /**实例
    struct DINFO
    {
    int c,p;
    bool operator < (const DINFO &a) const {
        return c>a.c;
        }
    };
    说明两个DINFO结构体互相比较的实质是比较其成员变量c， 并且成员变量c越小的DINFO结构体越大
    **/
    bool operator < (const mach &b)const{
        return y<b.y;
    }
}arr[MAXN];

//对x进行降序排序
bool cmp1(const mach s1,const mach s2){
    return s1.x>s2.x;
}

struct task{
    ll x,y;
}brr[MAXN];

//先x后y降序排序规则函数
bool cmp2(const task s1,const task s2){
    if(s1.x!=s2.x) return s1.x>s2.x;
    else return s1.y>s2.y;
}

multiset<mach>s;
ll N,M,cnt,sum;

int main()
{
    while(scanf("%lld%lld",&N,&M)!=EOF){
        s.clear();
        cnt=sum=0;

        //机器
        for(int i=1;i<=N;i++)
            scanf("%lld%lld",&arr[i].x,&arr[i].y);

        arr[N+1]=mach{-1,-1};
        //机器对x进行降序排序
        sort(arr+1,arr+1+N,cmp1);

        for(int i=1;i<=M;i++)
            scanf("%lld%lld",&brr[i].x,&brr[i].y);

        //任务先x后y降序排列
        sort(brr+1,brr+1+M,cmp2);

        ll tmp=1;

        for(int i=1;i<=M;i++){
            //如果机器的x比任务的x大，放到s中去
            while(arr[tmp].x>=brr[i].x) s.insert(arr[tmp++]);

            multiset<mach>::iterator it = s.lower_bound(mach{0,brr[i].y});
            if(it==s.end()) continue;
            sum+=(500*brr[i].x+2*brr[i].y);
            cnt++;
            s.erase(it);

        }
        printf("%lld %lld\n",cnt,sum);
    }
    return 0;
}
```
