# 栈
- `Last In First Out`先进后出
- 在表尾进行插入和删除
- 允许插入和删除的一端称为栈顶，另一端称为栈底
**线性栈是一个数组，空栈时top=-1**
## 栈的顺序存储结构
- `base` `top` `长度`
```C
typedef struct
{
  int data[MAXSIZE];
  int top;
}SqStack;

typdef struct
{
  int *base;
  int *top;
  int stacksize;
}SqStack;
```
- 构造空栈：分配存储空间，top=base，stacksize
```C
Status InitStack(SqStack *S)
{
  S->base = (int)malloc(STACK_INITSIZE *sizeof(int));
  if(!S->base) exit(OVERFLOW);
  S->top = S->base;
  S->stacksize = STACK_INIT_SIZE;
  return OK;
}
```
- 进栈
判断栈是否已满 栈顶+1
```C
Status Push(SqStack *S,int e)
{
  if(S->top == MAXSIZE - 1)
    return ERROR;
  S->top ++;
  s->data[s->top] = e;
  return OK;
}
```
- 出栈
```C
Status Pop(SqStack *S,int *e)
{
  if(S->top == -1)
    return ERROR;
  *e = S->data[S->top];
  S->top--;
  return OK;
}
```
- 两栈共享空间

## 链栈
- 存储结构
```C
typedef struct StackNode
{ //结点
  
  int data;
  struct StackNode *next;

}StackNode,*LinkStackptr;

```
```C
typedef struct StackNode
{
  LinkStackptr top;
  int count;
}LinkStack;
```
- 进栈
定义一个结点并开辟空间
把几点插入栈顶（表头）
栈顶存在的意义类似于头结点
```C
Status Push(LinkStack *S,int e)
{
  LinkStackPtr N = (LinkStackPtr)malloc(sizeof(StackNode));
  N->data = e;
  N->next = S->top;//?
  S->top = N;
  S->count ++;
  return OK;
}
```
- 出栈
定义一个结点q,赋给top,free(q),S->count--
```C
Status Pop(LinkStack *S,int e)
{
  LinkStackPtr q;
  if(StackEmpty(*S))
    return ERROR;
  *e = S->top->data;
  q = S->top;
  S->top = S->top->next;
  free(q);
  S->count--;
  return OK;
}
```
`int argc,char* argv[]`记录命令函参数和参数个数

## 栈的应用
1. 递归
- 后调用先返回，内存管理实行栈式管理
递归工作栈：递归过程执行过程中占用的
数据区。
- 递归工作记录：每一层的递归参数合成
一个记录。
- 当前活动记录：栈顶记录指示当前层的
执行情况。
- 当前环境指针：递归工作栈的栈顶指针。

**Fibonacci**
```C
#include "stdio.h"
int Fbi(int i)
{
  if(i<2)
    return i==0? 0:1;
  return Fbi(i-1)+Fbi(i-2);
}

int main(int argc,char* const argv[])
{
  for(int i=0;i<11;i++)
    printf("%d",Fbi(i));
  return 0;
}
```
**汉诺塔**
原问题：hanoi(n,A,B,C)
化简为：hanoi(n-1,A,C,B)把A上n-1个盘从A移动到C；
move(A,n,C)把第n个盘从A移动到C；
hanoi(n-1,B,A,C) 递归，把n-1个盘从B移动到C；
```C
void TowerOFHanoi(int n,char from_rod,char to_rod,char aux_rod )
{
  if(n == 1)
  {
    printf("\nMove disk i from rod %c to rod %c",from-rod_to)
    return;
  }
  TowerOfHanoi(n-1,from_rod,aux_rod,to_rod);
  printf("\nMove disk %d from rod %c to rod %c",n,from_rod,to_rod);//相当于move(A,n,C)
  TowerOfHanoi(n-1,aux_rod,to_rod,from_rod);//本质上都是从A移动到C
}
int main()
{
  int n = 3;
  TowerOfHanoi(3,'A','C','B');
  printf("\n");
  return 0;
}
```
**括号匹配检验**
**表达式求值**
后缀式求值：先找运算符，再找操作数
规则：从左到右遍历表达式的每个值，遇到数字进栈，遇到符号就将处于栈顶的两个元素出栈，进行运算，运算结果进栈
**迷宫问题求解**


