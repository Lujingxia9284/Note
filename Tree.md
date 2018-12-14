## 树
- 双亲表示法
```C
#define MAX_TREE_SIZE 100
typedef struct PTNode     //结点结构
{
  int data;      //数据
  int parent;    //双亲位置
}PTNode;

typedef struct
{
  PTNode nodes[MAX_TREE_SIZE]; //结点数组
  int r,n;   //根的位置和结点数
}PTree;
```
根结点没有双亲，位置域设为-1

- 孩子表示法
1. 树的度为指针域大小
2. 结点的度为指针域大小

把每个结点的孩子结点排列起来，以单链表作
存储结构，则 n 个结点有 n 个孩子链表，如果是叶子结点则此单
链表为空。然后 n 个头指针又组成一个线性表，采用顺序存储结
构，存放在一个一维数组中

```C
typedef MAX_TREE_SIZE 100
typedef struct CTnode   //定义孩子结点
{
  int child;          //数据域
  struct CTNode *next;   //指针域
}*ChildPtr  //定义为指针结构

typedef struct   //表头结构
{
  int data;              
  ChildPtr firstchild;   //头节点
}CTBox;

typedef struct
{
  CTBox nodes[MAX_TREE_SIZE];
  int r,n;     //根的位置和结点数
}CTree;
```
- 孩子兄弟表示法
设定两个指针指向该结点的孩子和右兄弟
```C
typedef struct CSNode
{
  int data;
  struct CSNode *firstchild,*rightsib;
}CSNode,*CSTree
```
---

## 二叉树
- 二叉树(Binary Tree)是 n (n ≥ 0) 个结点的有限集合，该
集合或者为空集（称为空二叉树），或是由一个根结点
加上两棵分别称为左子树和右子树的、互不交的二叉树
组成。
- 二叉树的特点
1. 每个结点最多有两颗子树（其中包含没有子树或者
有一棵子树），二叉树中不存在度大于2的结点。
2. 左子树和右子树是有顺序的，次序不能任意颠倒。
3. 即使树中只有一棵子树，也要区分左子树和右子树。
- 特殊二叉树：斜树，满二叉树（所有分支结点都存在左子树
和右子树，并且所有叶子都在同一层上），完全二叉树
- 完全二叉树的特点
1. 叶子结点只能出现在最下两层。
2. 最下层的叶子结点一定集中在左部连续位值。
3. 倒数第二层，若有叶子结点，一定都在右部连
续位值。
4. 如果结点度为1，则该结点只有左孩子，即不存
在只有右子树的情况。
5. 同样结点的二叉树，完全二叉树的深度最小。

---
## 二叉树的存储结构
### 一、二叉树的顺序存储表示

完全二叉树顺序存储，非完全二叉树补设“虚结点”，使得二叉树的结点的编号与完全二叉树相同，再进行顺序存储，造成存储空间浪费



### 二、链式存储结构
- 链式存储结构中结点的结构

|左孩子指针域|数据|右孩子指针域|
|:---:|:---:|:---:|
|lchild|data|rchild|

- 二叉链表
类型为node的结点，再加上一个指向根节点的头指针
```C
typedef struct node
{
  int data;
  struct node *lchild,*rchild;
} bitree;
bitree *root;
```

若二叉树为空，则
root = NULL ，在 n 个结点的二叉树中一共有 2n 个指针域， n+1 个为空，
n-1 个非空。

- 三叉链表（寻找某结点的双亲）

|左孩子指针域|数据|双亲|右孩子指针域|
|:---:|:---:|:---:|:---:|
|lchild|data|parent|rchild|

```C
typedef struct TriTNode{
  int data;
  struct *lchild,*rchild,*parent;
}TriTNode,*TriTree;
```

---
## 二叉树的遍历
指从根结点出发，按照某
种次序依次访问二叉树中所有结点，
使得每个结点被访问一次且仅被访
问一次。（先上后下，先左后右，先右后左）

|前序|中序|后序|
|:--:|:--:|:--:|
|根-左-右|左-根-右|左-右-根|


- 前序遍历：访问根节点，先序遍历左指数，先序遍历右指数
```C
void PreOrderTraverse(BiTree T)
{
  if(T==NULL)
    return;
  printf("%c",T->data);
  PreOrderTraverse(T->lchild);  //左子树
  PreOrderTraverse(T->rchild);  //右子树
}
```


- 中序遍历：中序遍历左子树，访问根结点，中序遍历右子树
```C
void InOrderTraverse(BiTree T)
{
  if(T==NULL)
    return;
    InOrderTraverse(T->lchild)
    print("%c\n",T->data);
    InOrderTraverse(T->rchild);
}
```
- 后序遍历左子树，后序遍历右子树，访问根结点
```C
void PostOrderTraverse(BiTree T)
{
  if(T == NULL)
    return;
  PostOrderTraverse(T->lchild);
  PoseOrderTraverse(T->rchild);
  printf("%c",T->data);
}
```
- 创建一个新的根结点
```C
BTNode *newnode(int data)
{
  BTNode *node = (BTNode *)malloc(sizeof(BTNode));
  node->data = data;
  node->lchild = NULLL;
  node->rchild = NULL;
}
```
- 层序遍历
##### 打印指定层
```C
void printGiverLevel(TNode *root,int level)
{
  if(root == NULL)
    return;
  if(level == 1)
    printf("%d",root->data);
  else if(level > 1)
  {
    printGiverLevel(root->left,level-1);
    printGivenLevel(root->right,level-1);
  }
}

```
##### 打印所有层
```C
void printLevelOrder(TNode *root,int height)
{
  for(int i=1;i<=height;i++)
    printGiverLevel(root,i);
}
```
---
## 遍历算法的应用
- 统计二叉树中叶子结点的个数
```C
void CountLeaf(BiTree T,int count)
{
  if(T){
    if((!T->lchild)&&(!T->rchild))
      count++;
    CountLeaf(T->lchild,count);
    CountLeaf(T->rchild,count);
  }
}
```
- 求二叉树的深度（后序遍历）

  二叉树的深度为其左右子树深度的最大值+1

  ```C
  int Depth(BiTree T){
    if(!T)  depthval = 0;
    else {
      depthLeft = Depth(T->lchild);
      depthRight = Depth(T->rchild);
      depthval = 1+(depthLeft>depthRight ? depthLeft:depthRight);
    }
    return depthval;
  }
  ```
- 复制二叉树
生成一个二叉树结点
```C
BiTNode *GetTreeNode(int item,BiTNode *lptr,BiTNode *rptr ){
  if(!(T = (BiTNode*)malloc(sizeof(BiTNode))))
    exit(0);
  T->data = item;
  T->lchild = lptr;
  T->rchild = rptr;
  return T;
}
```
复制
```C
BitNode *CopyTree(BiTNode *T){
  if(!T) return NULL;
  if(T->lchild)
    newlptr = CopyTree(T->lchild);
  else newlptr = NULL;
  if(T->rchild)
    newrptr = CopyTree(T->rchild);
  else newrptr = NULL;
  newT=GetTreeNode(T->data,newlptr,newrptr);
  return newT;
}
```
- 二叉树的建立
前提：完全二叉树，每个结点有两个或者零个孩子结点
##### 以字符串形式定义一个二叉树
```C
int CreatBiTree(BiTree *T){
  scanf(&ch);
  if(ch == '') T=NULL;
  else{
    if(!(T=（BiTNode *)malloc(sizeof(BiTNode)))
      exit(OVERFLOW);
    T->data = ch;
    CreateBiTree(T->lchild);
    CreateBiTree(T->rchild);
  }
  return OK;
}
```


















