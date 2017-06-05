// 多维数据的组合遍历

#include<iostream>
#include<stdio.h>
#include<string.h>

using namespace std;


int vars[]={
	2,3,5,7,11,
	13,17,19,23,29};
int varMax[]={
	10,9,8,7,6,
	5,4,3,2,1};

void TraversalByRecu(int dim, int ind, int max, int var[]){
	if(ind>=dim){
		for(int j=0; j<dim; j++){
			printf("%d\t",var[j]);
		}
		printf("\n");
		return;
	}
	int i;
	for(i=1;i<=max;i++){
		var[ind]=i;
		TraversalByRecu(dim,ind+1,varMax[ind+1],var);
	}	
}

int main(){
	freopen("out1.txt","w",stdout);
	int var[10];
	memset(var,0,sizeof(int)*10);
	TraversalByRecu(3,0,varMax[0],var);

	return 0;
}
