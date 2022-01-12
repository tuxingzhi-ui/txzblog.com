---
title: 数据结构一二章
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
```
void PrintN ( int N )
{/* 打印从1到N的全部正整数 */
	int i;
	for ( i=1; i<=N; i++ ){
		printf("%d\n", i );
	}
} 
```

1-2
```
void PrintN ( int N )
{/* 打印从1到N的全部正整数 */
	if ( N > 0 ){
		PrintN( N-1 ); 
		printf("%d\n", N );
	}
} 
```
1-3
```
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
```
1-4
```
double f( int n, double a[], double x )
{/* 计算阶数为n，系数为a[0]...a[n]的多项式在x点的值 */
	int i;
	double p = a[0];
	for ( i=1; i<=n; i++ )
		p += a[i] * pow(x, i);
	return p;
}
```
1-5
```
double f( int n, double a[], double x )
{/* 计算阶数为n，系数为a[0]...a[n]的多项式在x点的值 */
	int i;
	double p = a[n];
	for ( i=n; i>0; i-- )
		p = a[i-1] + x * p;
	return p;
}
```
1-6
```
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
```
1-7
```
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
```
1-8
```
vid SelectionSort ( int List[], int N )
{ /* 将N个整数List[0]...List[N-1]进行非递减排序 */
	int i;
	for ( i=0; i<N; i++ ) {
	    /* 从List[i]到List[N-1]中找最小元，并将其位置赋给MinPosition */
        MinPosition = ScanForMin( List, i, N-1 ); 

		/* 将未排序部分的最小元换到有序部分的最后位置 */
		Swap( List[i], List[MinPosition] );
	}
}
```
1-9
```
int IterativeSum ( int List[], int N )
{ /* 循环求N个整数的和 */
    int i ; /* 执行1步 */
    int Sum = 0; /* 执行1步 */

    for ( i=0; i<N; i++ ) /* 共执行N+1步 */
       Sum += List[i] ;  /* 共执行N步   */

	return Sum;  /* 执行1步 */
}
```
1-10
```
int RecursiveSum ( int List[], int N )
{ /* 递归求N个整数的和 */
	if ( N )   /* 执行1步 */
		return (RecursiveSum(List, N-1)+List[N-1]); /* 执行X+2步 */
    return 0;  /* 执行1步 */
}
```
1-11
```
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
```
1-12
```
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
```
1-13
```
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
```
1-14
```
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
```
2-1
```
ElementType Average( ElementType S[], int N )
{ /* 求N个集合元素S[]的平均值 */
	int i;
	ElementType Sum = 0;

    for ( i=0; i<N; i++ )
		Sum += S[i];  /* 将数组元素累加到Sum中 */

    return Sum/N;
}
```
2-2
```
ElementType FindKthLargest( ElementType S[], int K )
{ /* 此为伪代码 */	
	选取S中的第一个元素e;
	根据e将集合S（不包含e）分解为大于等于e的元素集合S1和小于e的元素集合S2;
	if ( |S1| >= K )       return FindKthLargest( S1, K );
	else if ( |S1| < K-1 ) return FindKthLargest( S2, K-|S1|-1 );
	else return e;  
}
```
2-3
```
ElementType Max( ElementType S[], int N )
{ /* 求N个集合元素S[]中的最大值 */
	int i;
	ElementType CurMax = S[0];

	for ( i=1; i<N; i++ )
		if ( S[i] > CurMax ) /* 若A[i]比当前最大值还要大 */
			CurMax = S[i];   /* 则更新当前最大值 */
	return CurMax;
}
```
2-4
```
#include <stdio.h>

int main()
{
	union key {
		int  k;
		char ch[2];
	} u;
	
	u.k = 258;
	printf("%d %d\n", u.ch[0],u.ch[1]);
	
	return 0;
}
```
2-4-1.h
```
/* 单向链表结点的定义 */

typedef struct Node *PtrToNode;
struct Node {
	ElementType Data; /* 存储结点数据 */
	PtrToNode   Next; /* 指向下一个结点的指针 */
};

/* 结点空间申请 */
PtrToNode p = (PtrToNode)malloc(sizeof(struct Node));

typedef PtrToNode List; /* 定义单链表类型 */
```
2-4-2.h
```
/* 双向链表结点的定义 */

typedef struct DNode *PtrToDNode;
struct DNode {
	ElementType Data;     /* 存储结点数据 */
	PtrToDNode  Next;     /* 指向下一个结点的指针 */
	PtrToDNode  Previous; /* 指向前一个结点的指针 */
};
```
2-5
```
List Reverse( List L )
{ /* 将单链表L逆转 */
	PtrToNode Old_head, New_head, Temp;

	Old_head = L;    /* 初始化当前旧表头为L */
	New_head = NULL; /* 初始化逆转后新表头为空 */
	while ( Old_head )  { /* 当旧表不为空时 */
		Temp = Old_head->Next;
		Old_head->Next = New_head;  
		New_head = Old_head; /* 将当前旧表头逆转为新表头 */
		Old_head = Temp;     /* 更新旧表头 */
	}
	L = New_head; /* 更新L */
	return L;
}
```
2-6
```
int FactorialSum( List L )
{ /* 求单链表L中所有结点Data的阶乘和 */
  /* 这里默认所有结点的Data值非负 */
	int Fact, Sum, i;
	PtrToNode P = L;

	Sum = 0;
	while ( P ) {
		Fact = 1;
		for ( i=2; i<=P->Data; i++ )
			Fact *= i;
		Sum += Fact;
		P = P->Next;
	}
	return Sum;
}
```
2-7
```
ElementType Median( ElementType A[], int N )
{
	int i, j, MaxPosition;
	ElementType TmpA;

	for ( i=0; i<N-1; i++ ) {
		MaxPosition = i;
		for ( j=i+1; j<N; j++ ) /* 内循环找出最大值的下标MaxPosition */
			if ( A[j] > A[MaxPosition] )  MaxPosition = j;
		/* 下面将最大值与待排序序列的第一个元素A[i]交换 */
		TmpA=A[i];  A[i]=A[MaxPosition];  A[MaxPosition]=TmpA;
	} /* 排序结束 */

    /* 数组中下标为(N-1)/2位置的元素就是序列中第N/2个元素 */
	return A[(N-1)/2];  
}
```
2-8
```
#include <stdio.h>

void Swap( int X, int Y )
{ /* 错误的交换函数 */
	int tmp;	
	tmp = X; X = Y; Y = tmp;
} 

int main()
{
	int X = 10, Y = 20;

	Swap( X, Y );
	printf("X = %d, Y = %d", X, Y);
	
	return 0;
}
```
2-9
```
#include <stdio.h>

void Swap( int *X, int *Y )
{ /* 正确的交换函数 */
	int tmp;
    tmp = *X; *X = *Y; *Y = tmp;
} 

int main()
{
    int X = 10, Y = 20;
    
	Swap( &X, &Y );
	printf("X = %d, Y = %d", X, Y);

	return 0;
}
```
2-10
```
int Factorial( int N )
{
	if ( N == 0 )
		return 1;
	else
		return N * Factorial(N-1);
}
```
2-11
```
void Move( int n, int start, int goal, int temp )
{
    if ( n > 1 ) {
		Move( n-1, start, temp, goal );
		printf("Move disk %d from %d to %d.\n", n, start, goal);
		Move( n-1, temp, goal, start );
	}
	/* else 当n==1时不需要做任何事 */
}
```
2-12
```
void Swap( ElementType *X, ElementType *Y )
{ /* 交换X和Y两个元素 */
	ElementType tmp;
    tmp = *X; *X = *Y; *Y = tmp;
} 

ElementType FindKthLargest ( ElementType S[], int K, int Left, int Right )
{  /* 在S[Left]...S[Right]中找第K大元素 */
	ElementType e = S[Left]; /* 简单取首元素为基准 */
	int L = Left, R = Right;

	while (1) { /* 将序列中比基准大的移到基准左边，小的移到右边 */
		while ( (Left<=Right)&&(e <= S[Left]) )  Left++;
		while ( (Left<Right)&&(e > S[Right]) )  Right--;
        if ( Left < Right )
		    Swap ( &S[Left], &S[Right] ) ;
		else  break;
	}
    Swap ( &S[Left-1], &S[L] ); /* 将基准换到两集合之间 */
	if ( (Left-L-1) >= K ) /* (Left-L-1)代表了集合S1的大小 */
		return FindKthLargest(S, K, L, Left-2); /* 在集合S1中找 */
	else if ( (Left-L-1) < K-1 ) 
		return FindKthLargest(S, K-(Left-L-1)-1, Left, R); /* 在集合S2中找 */
	else 
		return e;/* 找到，返回 */
}
```
2-13
```
ElementType Median( ElementType S[], int N )
{   
	return FindKthLargest(S, (N+1)/2, 0, N-1);
}
```