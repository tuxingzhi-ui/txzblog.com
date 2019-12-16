---
title: DataStructure第一章
author: TXZ from课件
date: '2019-12-16'
slug: datastructure
categories:
  - Hugo
tags:
  - Markdown
  - blogdown
---
1-1

void PrintN ( int N )
{/* 打印从1到N的全部正整数 */
	int i;
	for ( i=1; i<=N; i++ ){
		printf("%d\n", i );
	}
} 


1-2

#include <stdio.h>

/* "void PrintN ( int N )"可使用"1-1.c"或"1-2.c" */
void PrintN ( int N );

int main ()
{/* 读入整数N，并调用PrintN函数 */
	int N;
	scanf("%d", &N);
	PrintN( N );
	return 0;
}

1-3

#include <stdio.h>

/* "void PrintN ( int N )"可使用"1-1.c"或"1-2.c" */
void PrintN ( int N );

int main ()
{/* 读入整数N，并调用PrintN函数 */
	int N;
	scanf("%d", &N);
	PrintN( N );
	return 0;
}

1-4

double f( int n, double a[], double x )
{/* 计算阶数为n，系数为a[0]...a[n]的多项式在x点的值 */
	int i;
	double p = a[0];
	for ( i=1; i<=n; i++ )
		p += a[i] * pow(x, i);
	return p;
}

1-5

double f( int n, double a[], double x )
{/* 计算阶数为n，系数为a[0]...a[n]的多项式在x点的值 */
	int i;
	double p = a[n];
	for ( i=n; i>0; i-- )
		p = a[i-1] + x * p;
	return p;
}

1-6

#include <stdio.h>
#include <time.h>

clock_t  start, stop; /* clock_t是clock()函数返回的变量类型 */
double  duration;  /* 记录被测函数运行时间，以秒为单位 */

int main ()
{	/* 不在测试范围内的准备工作写在clock()调用之前*/

	start = clock(); /* 开始计时 */
	MyFunction(); 	 /* 把被测函数加在这里，使用时这个函数必须被替换 */
	stop = clock();	 /* 停止计时 */
	duration = ((double)(stop - start))/CLK_TCK; /* 计算运行时间 */
	/* 注意CLK_TCK是机器时钟每秒所走的时钟打点数， */
	/* 在某些IDE下也可能叫CLOCKS_PER_SEC。         */

    /* 其他不在测试范围的处理写在后面，例如输出duration的值 */
	return 0;
}

1-7

/* 给定9阶多项式 f(x)=1*x+2*(x^2)+...+9*(x^9) */
/* 用不同方法计算f(1.1)并且比较运行时间                         */

#include <stdio.h>
#include <time.h>
#include <math.h>

clock_t start, stop;
double duration;
#define MAXN 10  /* 多项式最大项数，即多项式阶数+1 */
#define MAXK 1e7 /* 被测函数最大重复调用次数*/

double f1( int n, double a[], double x )
{
	int i;
	double p = a[0];
	for ( i=1; i<=n; i++ )
		p += (a[i] * pow(x, i));
	return p;
}

double f2( int n, double a[], double x )
{
	int i;
	double p = a[n];
	for ( i=n; i>0; i-- )
		p = a[i-1] + x*p;
	return p;
}

void run( double (*f)( int, double*, double ), double a[], int case_n )
{/* 此函数用于测试被测函数(*f)的运行时间，并且根据case_n输出相应的结果 */
 /* case_n是输出的函数编号：1代表函数f1；2代表函数f2                   */
	int i;

	start = clock();
	for ( i=0; i<MAXK; i++ ) /* 重复调用函数以获得充分多的时钟打点数*/
		(*f)(MAXN-1, a, 1.1);
	stop = clock();

	duration = ((double)(stop - start))/CLK_TCK;
	printf("ticks%d = %f\n", case_n, (double)(stop - start));
	printf("duration%d = %6.2e\n", case_n, duration);
}

int main ()
{
	int i;
	double a[MAXN]; /* 存储多项式的系数*/

	/* 为本题的多项式系数赋值，即a[i]=i */
	for ( i=0; i<MAXN; i++ ) a[i] = (double)i;

	run(f1, a, 1);
	run(f2, a, 2);

	return 0;
}

1-8

void SelectionSort ( int List[], int N )
{ /* 将N个整数List[0]...List[N-1]进行非递减排序 */
	int i;
	for ( i=0; i<N; i++ ) {
	    /* 从List[i]到List[N-1]中找最小元，并将其位置赋给MinPosition */
        MinPosition = ScanForMin( List, i, N-1 ); 

		/* 将未排序部分的最小元换到有序部分的最后位置 */
		Swap( List[i], List[MinPosition] );
	}
}

1-9

int IterativeSum ( int List[], int N )
{ /* 循环求N个整数的和 */
    int i ; /* 执行1步 */
    int Sum = 0; /* 执行1步 */

    for ( i=0; i<N; i++ ) /* 共执行N+1步 */
       Sum += List[i] ;  /* 共执行N步   */

	return Sum;  /* 执行1步 */
}

1-10

int RecursiveSum ( int List[], int N )
{ /* 递归求N个整数的和 */
	if ( N )   /* 执行1步 */
		return (RecursiveSum(List, N-1)+List[N-1]); /* 执行X+2步 */
    return 0;  /* 执行1步 */
}

1-11

int MaxSubseqSum1( int List[], int N )
{
	int i, j, k;
	int ThisSum, MaxSum = 0;

	for ( i=0; i<N; i++ ) {     /* i是子列左端位置 */
		for ( j=i; j<N; j++ ) { /* j是子列右端位置 */
			ThisSum = 0;  /* ThisSum是从List[i]到List[j]的子列和 */
			for ( k=i; k<=j; k++ )
				ThisSum += List[k];
			if ( ThisSum > MaxSum ) /* 如果刚得到的这个子列和更大 */
				MaxSum = ThisSum;   /* 则更新结果 */
		} /* j循环结束 */
    } /* i循环结束 */
	return MaxSum;
}

1-12

int MaxSubseqSum2( int List[], int N )
{
	int i, j;
	int ThisSum, MaxSum = 0;

	for( i=0; i<N; i++ ) {     /* i是子列左端位置 */
		ThisSum = 0;  /* ThisSum是从List[i]到List[j]的子列和 */
		for( j=i; j<N; j++ ) { /* j是子列右端位置 */
			/*对于相同的i，不同的j，只要在j-1次循环的基础上累加1项即可*/
			ThisSum += List[j];
			if( ThisSum > MaxSum ) /* 如果刚得到的这个子列和更大 */
				MaxSum = ThisSum;   /* 则更新结果 */
		} /* j循环结束 */
    } /* i循环结束 */
	return MaxSum;
}

1-13

int Max3( int A, int B, int C )
{ /* 返回3个整数中的最大值 */
	return A > B ? A > C ? A : C : B > C ? B : C;
}

int DivideAndConquer( int List[], int left, int right )
{ /* 分治法求List[left]到List[right]的最大子列和 */
	int MaxLeftSum, MaxRightSum; /* 存放左右子问题的解 */
	int MaxLeftBorderSum, MaxRightBorderSum; /*存放跨分界线的结果*/

	int LeftBorderSum, RightBorderSum;
	int center, i;

	if( left == right ) {/* 递归的终止条件，子列只有1个数字 */
		if( List[left] > 0 )  return List[left];
		else return 0;
	}

    /* 下面是"分"的过程 */
	center = ( left + right ) / 2; /* 找到中分点 */
	/* 递归求得两边子列的最大和 */
	MaxLeftSum = DivideAndConquer( List, left, center );
	MaxRightSum = DivideAndConquer( List, center+1, right );

    /* 下面求跨分界线的最大子列和 */
	MaxLeftBorderSum = 0; LeftBorderSum = 0;
	for( i=center; i>=left; i-- ) { /* 从中线向左扫描 */
		LeftBorderSum += List[i];
		if( LeftBorderSum > MaxLeftBorderSum )
			MaxLeftBorderSum = LeftBorderSum;
	} /* 左边扫描结束 */

	MaxRightBorderSum = 0; RightBorderSum = 0;
	for( i=center+1; i<=right; i++ ) { /* 从中线向右扫描 */
		RightBorderSum += List[i];
		if( RightBorderSum > MaxRightBorderSum )
			MaxRightBorderSum = RightBorderSum;
	} /* 右边扫描结束 */

    /* 下面返回"治"的结果 */
	return Max3( MaxLeftSum, MaxRightSum, MaxLeftBorderSum + MaxRightBorderSum );
}

int MaxSubseqSum3( int List[], int N )
{ /* 保持与前2种算法相同的函数接口 */
	return DivideAndConquer( List, 0, N-1 );
}

1-14

int MaxSubseqSum4( int List[], int N )
{
	int i;
	int ThisSum, MaxSum;

	ThisSum = MaxSum = 0;
	for ( i=0; i<N; i++ ) {
		ThisSum += List[i]; /* 向右累加 */
		if ( ThisSum > MaxSum )
			MaxSum = ThisSum; /* 发现更大和则更新当前结果 */
		else if ( ThisSum < 0 ) /* 如果当前子列和为负 */
			ThisSum = 0; /* 则不可能使后面的部分和增大，抛弃之 */
	} 
	return MaxSum;
}