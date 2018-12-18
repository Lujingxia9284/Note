# 栈
- `Last In First Out`先进后出
- 在表尾进行插入和删除
- 允许插入和删除的一端称为栈顶，另一端称为栈底

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







