#include <iostream>

int main(int argc, char** argv) {
	int a,b;
	int pcd;
	scanf("%d%d",&a,&b);
	while(b!=0){
		int t=a%b;
		a=b;
		b=t;
	}
	printf("pcd=%d",a);
}
