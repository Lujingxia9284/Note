# 线性表
## 线性表的顺序存储结构
- **存储空间起始位置**
- **线性表最大容量listsize**
- **线性表当前长度length**
```C
typedef struct
{

  int data[MAXSIZE];    //数组存储数据元素
  int length;         //当前线性表长度

}SqList;
```
### 线性表的初始化
```C
Status InitList_Sq(Sq_List *L)
{
  L->elem = (int *)malloc(LIST_INIT_SIZE *sizeof(int));  //分配存储空间
  if（！L->elem）exit(OVERFLOW);  //分配失败
  L->length = 0;   //空表
  L->listsize = LIST_INIT_SIZE ;
}
```
### 线性表中元素的插入
>1.判断是否为满表
2.判断插入位置的合法性
3.当插入位置不在表尾时，插入位置定义一个指变量，从表尾开始逐个往后移
4.表长+1
```C
Status ListInsert_Sq(SqList *L, int i,int e)
{
  if(L->length == L->listsize) return ERROR;
  if(i<i || i>L->length+1)  return ERROR;
  if(i<=L->length)    //不在表尾插入
  {
    q = &(L->elem[i-1]);
    for(p = &(L->elem[length-1]);p>=q;--p)
      *(p+1) = *p;
    *q = e;
    ++L->length;
  }
  return 1; 
}
```
### 满表情况下元素插入
>重新分配存储空间，增加存储容量
```C
if（L->length == L->listsize）
{
  newbase = (int *)realloc(L->elem,(L->listsize+LISTINCREMENT) *sizeof(int));
  if(!newbase) exit(OVERFLOW);
  L->listsize += LISTINCREMENT;
}
```
```C
int GetElem(SqList L,int i)
{
  if( L.length == 0 || i<1 || i > length )
    return 0;
  return(L->elem[i-1]);
}
```
## 线性表的链式存储结构
>- 头结点放在第一个结点之前，数据域一般无意义，不是链表的必要元素
定义结点
```C
typedef struct Node{
  int data;
  struct Node *next;
}LNode,*LinkList
```
`LinkList L` 链表类型
`LNode`结点类型
>- 查找第i个结点并返回其值
   声明一个指针指向第一个结点
```C
Status GetElem(LinkList L,int i,int *e)
{
  int j = 1;
  LinkList p;
  p = L->next;   //声明一个指针指向链表的第一个结点
  while(p && j<i)
  {
    p = p->next;
    ++j;
  }
  if(!p || j > i)      //第i个结点不存在
    return ERROR;
  *e = p->data;
  return OK;
}
```
>- 在L中第i个结点之前里插入数据元素e,定义一个指针p指向第i-1个元素，生成一个结点s插入
```C
Status ListInert(LinkList L,int i,int e){
  int j = 1;
  LinkList p,s;
  p = L;
  while(p && j<i)
  {
    p = p->next;
    ++j;
  }
  if(!p || j>i)
    return ERROR;
  s=(LinkList)malloc(sizeof(LNode));
  s->data = e
  s->next = p->next;
  p->next = s;
  return OK;
}
```
>- 删除第i个结点并返回其值
找到第i-1个结点p,和第i个结点q,将p的后继赋给q的后继，然后释放q
```C
Status ListDelete(LinkList L,int i,int *e)
{
  int j=1;
  LinkList p,q;
  p = L;
  while(p->next && j<i)
  {
    p = p->next;
    ++j;
  }
  q = p->next;
  p->next = q->next;
  *e = q->data;
  free(q);
  return OK;
}
```

### 单链表的整表创建
- 头插法
生成一个长度为n带头结点的单链表L,L->next = NULL，再创建新结点，插入到L->next
```C
void CreatListHead(LinkList L,int n){
  
  LinkList p;
  srand(time(0));
  L = (LinkList)malloc(sizeof(LNode));
  L->next = NULL;
  for(int i=0;i<n;i++)
  {
    p = (LinkList)malloc(sizeof(LNode));
    p->data = rand()%100 + 1；
    p->next = L->next;
  }
  return OK;
}
- 尾插法
定义一个结点r始终为表尾结点，生成新结点p插入到r->next,再将pf赋给r
```C
void CreatListTail(LinkList L，int n)
{
  LinkList p,r;
  int 1
  srand(time(0));
  L = (LinkList)malloc(sizeof(LNode));
  L->next = NULL;
  for(i=0;i<n;i++)
  {
    p = (LinkList)malloc(sizeof(LNode));
    p->data = rand()%100 + 1;
    r->next = p;
    r = p;
  }
  r->next = NULL;   //当前链表结束
  return OK;
}
```
- 单链表的整表删除
定义一个指针p指向第一个结点，另一个指针q指向p->next，free（q），然后再把q赋给p
```C
Status ClearList(LinkList L)
{
  LinkList p,q;
  p = L->next;
  while(p)
  {
    q = p->next;
    free(q);
    p = q;
  }
  L->next = NULL;
}
```

静态链表/循环链表/双向链表/一元多项式的的表示







