#include<iostream>
#include<stdio.h>
using namespace std;

static const int little_prime[] = {
2,3,5,7,11,13,17,19,23,29,
31,37,41,43,47,53,59,61,67,71
};

// 求大数n约数的个数
int NumOfFac(long long n);

// 求不超过数n的约数最多的最小的数
long long minN;
int numOfMinN;
void FindMinN(long long low, long long high, long long n, int counts, int len, int maxTimes);

int main(){
	freopen("in.txt","r",stdin);		//redirect the input stream
	
	long long i,a,b,min=0;
	int count = 0;
	scanf("%lld %lld",&a,&b);

	FindMinN(a, b, 1, 1, 0, 60);
	printf("%lld\t%d\n", minN,numOfMinN);

		
		
		
	return 0;
}


// 快速计算n的约数个数
int NumOfFac(long long n){
	unsigned int i,k,count=1;
	long long m=n;
	while(m!=1){
		for(i=2; i<=m; i+=2){
			if(m % i == 0){
				k=1;
				while(m % i == 0){
					k++;
					m = m / i;
				}
				count = count*k;
			}
			// 2,3,5,7,11...避开2->3之间差1
			if(i == 2)
				i--;
		}
	}
	return count;
}


void FindMinN(long long low, long long high, long long n, int counts, int len, int maxTimes){
	// update
	if(n<=high && n>=low){
		if(counts > numOfMinN || (counts == numOfMinN && minN > n)){
			numOfMinN = counts;
			minN = n;
		}
	}

	// find
	int i;
	for(i=1; i<=maxTimes; i++){
		n = n * little_prime[len];
		if(n > high)
			break;
		FindMinN(low, high, n, counts*(i+1), len+1, i);
	}
}
