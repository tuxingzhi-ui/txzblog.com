---
title: DataStructure第三章
author: TXZ from课件
date: '2019-12-23'
slug: datastructure第三章
categories:
  - Example
tags:
  - Markdown
---

3-0-1
```
1.	List MakeEmpty()：初始化一个新的空线性表。
2.	ElementType FindKth( List L, int K )：根据指定的位序K，返回L中相应元素。
3.	Position Find( List L, ElementType X )：已知X，返回线性表L中与X相同的第一个元素的位置；若不存在则返回错误信息。
4.	bool Insert( List L, ElementType X, Position P )：在L的指定位置P前插入一个新元素X；成功则返回true，否则返回false。
5.	bool Delete( List L, Position P )：从L中删除指定位置P的元素；成功则返回true，否则返回false。
6.	int Length( List L )：返回线性表L的长度。

3-0-2
typedef int Position;
typedef struct LNode *PtrToLNode;
struct LNode {
	ElementType Data[MAXSIZE];
	Position Last;
};
typedef PtrToLNode List;
```

3-1
```
List MakeEmpty()
{
	List L;

	L = (List)malloc(sizeof(struct LNode));
	L->Last = -1;

	return L;
}
```
3-2
```
#define ERROR -1

Position Find( List L, ElementType X )
{
	Position i = 0;

	while( i <= L->Last && L->Data[i]!= X )
		i++;
	if ( i > L->Last )  return ERROR; /* 如果没找到，返回错误信息 */
	else  return i;  /* 找到后返回的是存储位置 */
}
```
3-3
```
bool Insert( List L, ElementType X, int i )
{ /* 在L的指定位序i前插入一个新元素X;位序i元素的数组位置下标是i-1 */
	Position j;

	if ( L->Last == MAXSIZE-1) {
		/* 表空间已满，不能插入 */
		printf("表满"); 
		return false; 
	}  
	if ( i<1 || i>L->Last+2 ) { 
    /* 检查插入位序的合法性：是否在1~n+1。n为当前元素个数，即Last+1 */
		printf("位序不合法");
		return false; 
	} 
	for( j=L->Last; j>=i-1; j-- ) /*Last指向序列最后元素 */
		L->Data[j+1] = L->Data[j]; /* 将位序i及以后的元素顺序向后移动 */
	L->Data[i-1] = X;  /* 新元素插入第i位序，其数组下标为i-1 */
	L->Last++;       /* Last仍指向最后元素 */
	return true; 
}
```
3-4
```bool Delete( List L, int i )
{ /* 从L中删除指定位序i的元素,该元素数组下标为i-1 */
	Position j;

	if( i<1 || i>L->Last+1 ) { /* 检查空表及删除位序的合法性 */
		printf("位序%d不存在元素", i ); 
		return false; 
	}
	for( j=i; j<=L->Last; j++ )    
		L->Data[j-1] = L->Data[j]; /*将位序i+1及以后的元素顺序向前移动*/
	L->Last--; /* Last仍指向最后元素 */
	return true;   
}
```
3-4-1
```
typedef struct LNode *PtrToLNode;
struct LNode {
	ElementType Data;
	PtrToLNode Next;
};
typedef PtrToLNode Position;
typedef PtrToLNode List;
```
3-5
```
int Length( List L )
{
	Position p;
	int cnt = 0; /* 初始化计数器 */

	p = L;  /* p指向表的第一个结点 */
	while ( p ) { 
		p = p->Next; 
		cnt++; /* 当前p指向的是第cnt个结点*/
	}   

	return cnt;
}
```
3-6
```
#define ERROR -1

ElementType FindKth( List L, int K )
{ /* 根据指定的位序K，返回L中相应元素 */
	Position p;
	int cnt = 1; /* 位序从1开始 */

	p = L; /* p指向L的第1个结点 */
	while ( p && cnt<K ) {
		p = p->Next;
		cnt++;  
	}
	if ( (cnt==K) && p )
		return p->Data; /* 找到第K个 */
	else
		return ERROR;   /* 否则返回错误信息 */
}
```
3-7
```
#define ERROR NULL

Position Find( List L, ElementType X )
{
	Position p = L; /* p指向L的第1个结点 */

	while ( p && p->Data!=X )
		p = p->Next;

	/* 下列语句可以用 return p; 替换 */
	if ( p )
		return p;
	else
		return ERROR;
}
```
3-8
```
#define ERROR NULL /* 用空地址表示错误 */

List Insert( List L, ElementType X, int i )
{	Position tmp, pre;

	tmp = (Position)malloc(sizeof(struct LNode)); /* 申请、填装结点 */
	tmp->Data = X; 
	if ( i == 1 ) { /* 新结点插入在表头 */
		tmp->Next = L;
		return tmp; /* 返回新表头指针 */
    }
	else {
		/* 查找位序为i-1的结点 */		
        int cnt = 1;  /* 位序从1开始 */
	    pre = L;      /* pre指向L的第1个结点 */
	    while ( pre && cnt<i-1 ) {
		    pre = pre->Next;
		    cnt++;  
	    }
		if ( pre==NULL || cnt!=i-1) { /* 所找结点不在L中 */
			printf("插入位置参数错误\n");
			free(tmp);
			return ERROR;
		}
		else { /* 找到了待插结点的前一个结点pre */
			/* 插入新结点，并且返回表头L */
			tmp->Next = pre->Next;
			pre->Next = tmp;
			return L;
		}
	}
}
```
3-9
```
bool Insert( List L, ElementType X, int i )
{ /* 这里默认L有头结点 */
	Position tmp, pre;
int cnt = 0;
	
/* 查找位序为i-1的结点 */		
	pre = L;      /* pre指向表头 */
	while ( pre && cnt<i-1 ) {
		    pre = pre->Next;
		    cnt++;  
	}
	if ( pre==NULL || cnt!=i-1) { /* 所找结点不在L中 */
		printf("插入位置参数错误\n");
		return false;
	}
	else { /* 找到了待插结点的前一个结点pre；若i为1，pre就指向表头 */
		/* 插入新结点 */
		tmp=(Position)malloc(sizeof(struct LNode)); /*申请、填装结点*/
		tmp->Data = X; 
		tmp->Next = pre->Next;
		pre->Next = tmp;
		return true;
	}
}
```
3-10
```
bool Delete( List L, int i )
{   /* 这里默认L有头结点 */
	Position tmp, pre;
    int cnt = 0;
	
    /* 查找位序为i-1的结点 */		
	pre = L;      /* pre指向表头 */
	while ( pre && cnt<i-1 ) {
		    pre = pre->Next;
		    cnt++;  
	}
	if ( pre==NULL || cnt!=i-1 ||pre->Next==NULL) {
    /* 所找结点或位序为i的结点不在L中 */
		printf("插入位置参数错误\n");
		return false;
	} else { /* 找到了待删结点的前一个结点pre */
		/* 将结点删除 */
		tmp=pre->Next;
        pre->Next=tmp->Next;
		free(tmp);
		return true;
	}
}
```
3-10-1
```
typedef struct GNode *PtrToGNode;
typedef PtrToGNode GList;
struct GNode {
	int Tag; /* 标志域：0表示该结点是单元素；1表示该结点是广义表 */
	union {
		/* 子表指针域Sublist与单元素数据域Data复用，即共用存储空间 */
		ElementType Data;
		GList    Sublist;
	} URegion;
	PtrPtrToGNode Next; /* 指向后继结点 */
};
```
3-10-2
```
typedef enum {Head, Term} NodeTag;

struct TermNode { /* 非零元素结点 */
	int Row, Col;
	ElementType Value;
};

typedef struct MNode *PtrToMNode;
struct MNode { /* 矩阵结点定义 */
	PtrToMNode Down, Right;
	NodeTag Tag;
	union { /* Head对应Next指针；Term对应非零元素结点 */
		PtrToMNode Next;
		struct TermNode Term;
	} URegion;
};
typedef PtrToMNode Matrix; /* 稀疏矩阵类型定义 */
Matrix  HeadNode [MAXSIZE]; /* MAXSIZE是矩阵最大非0元素个数 */
```
3-10-3
```
1.	Stack CreateStack( int MaxSize )： 生成空堆栈，其最大长度为MaxSize。
2.	bool IsFull( Stack S )：判断堆栈S是否已满。若S中元素个数等于MaxSize时返回true；否则返回false。
3.	bool Push( Stack S, ElementType X )：将元素X压入堆栈。若堆栈已满，返回false；否则将数据元素X插入到堆栈S栈顶处并返回true。
4.	bool IsEmpty ( Stack S )：判断堆栈S是否为空，若是返回true；否则返回false。
5.	ElementType Pop( Stack S )：删除并返回栈顶元素。若堆栈为空，返回错误信息；否则将栈顶数据元素从堆栈中删除并返回。

```
3-10-4
```
typedef int Position;
typedef struct SNode *PtrToSNode;
struct SNode {
	ElementType *Data; /* 存储元素的数组 */
	Position Top;      /* 栈顶指针 */
	int MaxSize;       /* 堆栈最大容量 */
};
typedef PtrToSNode Stack;
```
3-11
```
Stack CreateStack( int MaxSize )
{
	Stack S = (Stack)malloc(sizeof(struct SNode));
	S->Data = (ElementType *)malloc(MaxSize * sizeof(ElementType));
	S->Top = -1;
	S->MaxSize = MaxSize;
	return S;
}
```
3-12
```
bool IsFull( Stack S )
{
	return (S->Top == S->MaxSize-1);
}

bool Push( Stack S, ElementType X )
{
	if ( IsFull(S) ) {
		printf("堆栈满");
		return false;
	}
	else {
		S->Data[++(S->Top)] = X;
        return true;
    }
}
```
3-13
```
bool IsEmpty( Stack S )
{
	return (S->Top == -1);
}

ElementType Pop( Stack S )
{
	if ( IsEmpty(S) ) {
		printf("堆栈空");
		return ERROR; /* ERROR是ElementType的特殊值，标志错误 */
	}
	else 
		return ( S->Data[(S->Top)--] );
}
```
3-14
```
bool Push( Stack S, ElementType X, int Tag )
{ /* Tag作为区分两个堆栈的标志，取值为1和2 */
	if ( S->Top2-S->Top1 == 1) { /* 堆栈满 */
		printf("堆栈满\n");
		return false;
	}
	else {
		if ( Tag == 1 ) /* 对第一个堆栈操作 */
			S->Data[++(S->Top1)] = X;
		else              /* 对第二个堆栈操作 */
			S->Data[--(S->Top2)] = X;
		return true;
	}
}

ElementType Pop( Stack S, int Tag )
{ /* Tag作为区分两个堆栈的标志，取值为1和2 */
	if ( Tag == 1 ) { /* 对第一个堆栈操作 */
		if ( S->Top1 == -1 ) { /* 堆栈1空 */
			printf("堆栈1空\n");
			return ERROR;
		}
		else return S->Data[(S->Top1)--];
	}
	else { /* 对第二个堆栈操作 */
		if ( S->Top2 == S->MaxSize ) { /* 堆栈2空 */
			printf("堆栈2空\n");
			return ERROR;
		}
		else  return S->Data[(S->Top2)++];
	}
}
```
3-14-1
```
typedef struct SNode *PtrToSNode;
struct SNode {
	ElementType Data;
	PtrToSNode Next;
};
typedef PtrToSNode Stack;
```
3-15
```
Stack CreateStack( ) 
{ /* 构建一个堆栈的头结点，返回该结点指针 */
	Stack S;

	S = malloc(sizeof(struct SNode));
	S->Next = NULL;
	return S;
}

bool IsEmpty ( Stack S )
{ /* 判断堆栈S是否为空，若是返回true；否则返回false */
	return ( S->Next == NULL );
}

bool Push( Stack S, ElementType X )
{ /* 将元素X压入堆栈S */
	PtrToSNode TmpCell;

	TmpCell = (PtrToSNode)malloc(sizeof(struct SNode));
	TmpCell->Data = X;
	TmpCell->Next = S->Next;
	S->Next = TmpCell;
	return true;
}

ElementType Pop( Stack S )  
{ /* 删除并返回堆栈S的栈顶元素 */
	PtrToSNode FirstCell;
	ElementType TopElem;

	if( IsEmpty(S) ) {
		printf("堆栈空"); 
		return ERROR;
	}
	else {
		FirstCell = S->Next; 
		TopElem = FirstCell->Data;
		S->Next = FirstCell->Next;
		free(FirstCell);
		return TopElem;
	}
}
```
3-16
```
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

#define MAXOP 100    /* 操作数序列可能的最大长度 */
#define INFINITY 1e9 /* 代表正无穷 */
typedef double ElementType; /* 将堆栈的元素类型具体化 */
/* 类型依次对应运算数、运算符、字符串结尾 */
typedef enum {num, opr, end} Type;


/* 关于顺序堆栈的代码请参见顺序堆栈的定义和代码3.11-13，在此略去 */

/*****以下不出现在教材正文里*******/
typedef enum {true, false} bool;

typedef int Position;
struct SNode {
	ElementType *Data; /* 存储元素的数组 */
	Position Top;      /* 栈顶指针 */
	int MaxSize;       /* 堆栈最大容量 */
};
typedef struct SNode *Stack;

#define ERROR -1 /* 当堆栈为空时返回错误，这里默认正确返回值全是正的 */

#include "3-11.h"
#include "3-12.h"
#include "3-13.h"
/*****以上不出现在教材正文里*******/


Type GetOp( char *Expr, int *start, char *str )
{ /* 从*start开始读入下一个对象（操作数或运算符），并保存在字符串str中 */
	int i = 0;

    /* 跳过表达式前空格 */
	while ( (str[0]=Expr[(*start)++]) == ' ' ) ;

	while ( str[i]!=' ' && str[i]!='\0' )
		str[++i] = Expr[(*start)++];
	if ( str[i]=='\0' ) /* 如果读到输入的结尾 */
		(*start)--;     /* *start指向结束符 */
	str[i] = '\0';      /* 结束一个对象的获取 */

	if ( i==0 ) return end; /* 读到了结束 */
	else if( isdigit(str[0]) || isdigit(str[1]) ) /* 如果str[0]是数字、或是符号跟个数字 */
		return num;        /* 表示此时str中存的是一个数字 */
	else                   /* 如果str不是空串，又不是数字 */
		return opr;        /* 表示此时str中存的是一个运算符 */
}

ElementType PostfixExp( char *Expr )
{ /* 调用GetOp函数读入后缀表达式并求值 */
    Stack S;
	Type T;	
	ElementType Op1, Op2;
	char str[MAXOP];
	int start = 0;

	/* 申请一个新堆栈 */
	S = CreateStack( MAXOP );

	Op1 = Op2 = 0;
    while( (T=GetOp(Expr, &start, str)) != end ) { /* 当未读到输入结束时 */
		if ( T==num )
			Push( S, atof(str) );
		else {
			if ( !IsEmpty(S) ) Op2 = Pop(S);
			else Op2 = INFINITY;
			if ( !IsEmpty(S) ) Op1 = Pop(S);
			else Op2 = INFINITY;
			switch ( str[0] ) {
			case '+': Push(S, Op1 + Op2);  break;
			case '*': Push(S, Op1 * Op2);  break;
			case '-': Push(S, Op1 - Op2);  break;
			case '/': 
				if( Op2 != 0.0 ) /* 检查除法的分母是否为0 */
					Push(S, Op1/Op2);
				else {
					printf("错误：除法分母为零\n");
					Op2 = INFINITY;
				}
				break;
			default:
				printf("错误：未知运算符%s\n", str); 
				Op2 = INFINITY;
				break;
			}
			if ( Op2 >= INFINITY ) break;
		}
	}
	if ( Op2<INFINITY )      /* 如果处理完了表达式 */
		if ( !IsEmpty(S) )   /* 而此时堆栈正常 */
			Op2 = Pop(S);    /* 记录计算结果 */
		else Op2 = INFINITY; /* 否则标记错误 */
	free(S);    /* 释放堆栈 */
	return Op2;
}

int main()
{	
	char Expr[MAXOP];
	ElementType f;

	gets(Expr);
	f = PostfixExp(Expr);
	if ( f < INFINITY )
		printf("%.4f\n", f);
	else
		printf("表达式错误\n");

	return 0;
}
```
3-16-1
```
1.	Queue CreateQueue( int MaxSize )： 生成空队列，其最大长度为MaxSize。
2.	bool IsFull( Queue Q )：判断队列Q是否已满。若是返回true；否则返回false。
3.	bool AddQ( Queue Q, ElementType X )：将元素X压入队列Q。若队列已满，返回false；否则将数据元素X插入到队列Q并返回true。
4.	bool IsEmpty( Queue Q )：判断队列Q是否为空，若是返回true；否则返回false。
5.	ElementType DeleteQ( Queue Q )：删除并返回队列头元素。若队列为空，返回错误信息；否则将队列头数据元素从队列中删除并返回。

```
3-16-2
```
typedef int Position;
typedef struct QNode *PtrToQNode;
struct QNode {
	ElementType *Data;     /* 存储元素的数组 */
	Position Front, Rear;  /* 队列的头、尾指针 */
	int MaxSize;           /* 队列最大容量 */
};
typedef PtrToQNode Queue;
```
3-17
```
Queue CreateQueue( int MaxSize )
{
	Queue Q = (Queue)malloc(sizeof(struct QNode));
	Q->Data = (ElementType *)malloc(MaxSize * sizeof(ElementType));
	Q->Front = Q->Rear = 0;
	Q->MaxSize = MaxSize;
	return Q;
}

bool IsFull( Queue Q )
{
	return ((Q->Rear+1)%Q->MaxSize == Q->Front);
}

bool AddQ( Queue Q, ElementType X )
{
	if ( IsFull(Q) ) {
		printf("队列满");
		return false;
	}
	else {
		Q->Rear = (Q->Rear+1)%Q->MaxSize;
		Q->Data[Q->Rear] = X;
		return true;
	}
}

bool IsEmpty( Queue Q )
{
	return (Q->Front == Q->Rear);
}

ElementType DeleteQ( Queue Q )
{
	if ( IsEmpty(Q) ) { 
		printf("队列空");
		return ERROR;
	}
	else  {
		Q->Front =(Q->Front+1)%Q->MaxSize;
		return  Q->Data[Q->Front];
	}
} 
```
3-17-1
```
typedef struct Node *PtrToNode;
struct Node { /* 队列中的结点 */
	ElementType Data;
	PtrToNode Next;
};
typedef PtrToNode Position;

typedef struct QNode *PtrToQNode;
struct QNode {
	Position Front, Rear;  /* 队列的头、尾指针 */
	int MaxSize;           /* 队列最大容量 */
};
typedef PtrToQNode Queue;
```
3-18
```
bool IsEmpty( Queue Q )
{
	return ( Q->Front == NULL);
}

ElementType DeleteQ( Queue Q )
{
	Position FrontCell; 
	ElementType FrontElem;
	
	if  ( IsEmpty(Q) ) {
		printf("队列空");
		return ERROR;
	}
	else {
		FrontCell = Q->Front;
		if ( Q->Front == Q->Rear ) /* 若队列只有一个元素 */
			Q->Front = Q->Rear = NULL; /* 删除后队列置为空 */
		else                     
			Q->Front = Q->Front->Next;
		FrontElem = FrontCell->Data;

		free( FrontCell );  /* 释放被删除结点空间  */
		return  FrontElem;
	}
}
```
3-19
```
int Compare( int e1, int e2 )
{ /*比较两项指数e1和e2，根据大、小、等三种情况分别返回1，-1，0 */
	if ( e1 > e2 ) return 1;       /* e1大，返回1       */
	else if ( e1 < e2 ) return -1; /* e2大，返回-1      */
	else  return 0;                /* e1和e2相等，返回0 */
}

void Attach( int coef, int expon, Polynomial *PtrRear )  
{ /* 由于在本函数中需要改变当前结果表达式尾项指针的值，  */
  /* 所以函数传递进来的是结点指针的地址，*PtrRear指向尾项*/
	Polynomial P; 

	/* 申请新结点，并赋值 */
	P =(Polynomial)malloc(sizeof(struct PolyNode));
	P->coef = coef;
	P->expon = expon;
	P->link = NULL;
    /* 将P指向的新结点插入到当前结果表达式尾项的后面  */ 
	(*PtrRear)->link = P; 
	*PtrRear = P;   /* 修改PtrRear值 */
}

Polynomial PolyAdd(Polynomial P1, Polynomial P2)
{
	Polynomial front, rear, temp;
	int sum;
	
	/* 为方便表头插入，先产生一个临时空结点作为结果多项式链表头 */
	rear = (Polynomial)malloc(sizeof(struct PolyNode));  
	front = rear; /* 由front 记录结果多项式链表头结点 */
	while ( P1 && P2 )  /* 当两个多项式都有非零项待处理时 */
		switch ( Compare(P1->expon, P2->expon) ) {
			case 1: /* P1中的数据项指数较大 */
				Attach( P1->coef, P1->expon, &rear);
				P1 = P1->link;
				break;
			case -1: /* P2中的数据项指数较大 */
				Attach(P2->coef, P2->expon, &rear); 
				P2 = P2->link;
				break;
			case 0:  /* 两数据项指数相等 */
				sum = P1->coef + P2->coef;
				if ( sum ) Attach(sum, P1->expon, &rear);
				P1 = P1->link; 
				P2 = P2->link;
				break;
	}
	/* 将未处理完的另一个多项式的所有节点依次复制到结果多项式中去 */
	for ( ; P1; P1 = P1->link ) Attach(P1->coef, P1->expon, &rear);
	for ( ; P2; P2 = P2->link ) Attach(P2->coef, P2->expon, &rear);
	rear->link = NULL; 
	temp = front;
	front = front->link; /*令front指向结果多项式第一个非零项 */
	
	free(temp);    /* 释放临时空表头结点 */
	return front;
} 
```
3-19-1
```
#define MAXMATRIXSIZE 100 /* 迷宫矩阵最大行列数 */
#define MAXSTACKSIZE  100 /* 堆栈最大规模 */

struct Offsets { /* 偏移量结构定义 */
	short int Vert;   /* 纵向偏移 */
	short int Horiz;  /* 横向偏移 */
};

struct MazePosition {  /* 迷宫中的位置结构 */
	short int Row; /* 行号 */
	short int Col; /* 列号 */
	short int Dir; /* 对应偏移量数组的方向号 */
};
typedef struct MazePosition ElementType; /* 堆栈元素类型 */

/****       以下不出现在教材正文中      ****/
typedef int Position;
struct SNode {
	ElementType *Data; /* 存储元素的数组 */
	Position Top;      /* 栈顶指针 */
	int MaxSize;       /* 堆栈最大容量 */
};
typedef struct SNode *Stack;
/****       以上不出现在教材正文中      ****/
/* 正文援引代码3.11-13，对应CreateStack、IsEmpty、IsFull、Push和Pop */
/* 注意：由于从堆栈弹出的路径是反向的，所以我们从出口向入口反向搜索比较方便，
  这里不可以直接操纵堆栈内部元素。*/
```
3-20
```
void Path( int Maze[][MAXMATRIXSIZE], int EXITROW, int EXITCOL )
{ /* 默认迷宫Maze的入口为(1, 1)，出口为(EXITROW, EXITCOL) */
	/* 迷宫8个方向的偏移量数组 */
	struct Offsets Move[8] =
	{{-1, 0}, {-1, 1}, {0, 1}, {1, 1}, {1, 0}, {1, -1}, {0, -1}, {-1, -1}};
	int Mark[MAXMATRIXSIZE][MAXMATRIXSIZE]; /* 标记位置是否走过 */
	Stack S;  /* 辅助求解的堆栈 */
	struct MazPosition P;
	short int Row, Col, NextRow, NextCol, Dir;
	bool Found = false;

	S= CreateStack( MAXSTACKSIZE ); /* 初始化空堆栈 */

	Mark[EXITROW][EXITCOL] = 1; /* 从出口位置开始，标记为走过 */
	/* 将出口位置及下一个方向放入堆栈 */
	P.Row = EXITROW; 
	P.Col = EXITCOL;
	P.Dir = 0;
	Push( S, P );
    
	while ( !IsEmpty(S) && !Found ) { /* 当栈非空且没找到入口时 */
		P = Pop(S); /* 取出栈顶元素为当前位置 */
		Row = P.Row; Col = P.Col; Dir = P.Dir;
		while ( Dir < 8 && !Found ) {/* 当还有方向可探且没找到入口时 */
			/* 尝试往下一个方向Dir移动 */
			NextRow = Row + Move[Dir].Vert;
			NextCol = Col + Move[Dir].Horiz;
			if ( NextRow==1 && NextCol==1 )  
				/* 如果到达入口 */
				Found = true;
			else  /* 下一个位置不是入口 */
				/* 若下一个位置可通，且没走过 */
				if ( !Maze[NextRow][NextCol] && !Mark[NextRow][NextCol] ){					
					Mark[NextRow][NextCol] = 1; /* 标记为走过 */
					/* 当前位置和下一个方向存入栈 */
					P.Row = Row;
					P.Col = Col;
					P.Dir = Dir + 1;
					Push(S, P);
					/* 更新当前位置，从方向0开始 */
					Row = NextRow; Col = NextCol; Dir = 0;
				} /* 结束if */
				else ++Dir; /* 若此路不通，则在当前位置尝试下一个方向 */
		} /* 结束8方向探测 */
	} /* 结束搜索 */
	if ( Found ) { /* 找到一个路径，并输出该路径 */
		printf("找到路径如下\n");
		printf("行 列\n");
		printf("1  1\n"); /* 打印入口 */
		printf("%d  %d\n", Row, Col); /* 不要忘记最后一步未入堆栈 */
		while ( !IsEmpty(S) ) {
			P = Pop(S);
			printf("%d  %d\n", P.Row, P.Col);
		}
	}
	else /* 若没找到路径 */
		printf("该迷宫无解。\n");
}
```
