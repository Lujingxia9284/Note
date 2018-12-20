## 查找
1. 静态查找:集合中记录是固定的，没有插入和删除，只有查找
- 顺序查找:复杂度O(n)
- 二分查找：n个数据满足有序并且是连续存放（数组），可以进行二分查找,复杂度O（logN）
**在表中查找关键字为K的数据元素**
```C
int BinarySearch(List L,int K)
{
    int mid,left,right,NotFound = -1;
    left = 1;
    right = L->length;
    while(left<=right)   //元素必须顺序排列
    {
        mid = (left+right)/2;
        if(K<L->elem[mid])
            right = mid - 1;//修改右指针
        else if(K>L->elem[mid])
            left = mid + 1;//修改左指针
        else return mid;
    }
    return NotFound;
}
```
2. 动态查找：集合中记录是动态变化的，除了查找，还可能发生插入和删除

## 树
1. 结点的度：结点的子树个数
2. 树的度：树的所有结点中最大的度数
3. 叶结点：度为0的结点

- 儿子兄弟表示法
每个结点包含一个数据域，两个指针域

## 二叉树的存储结构
1. 顺序存储结构（数组）
完全二叉树
一般二叉树补齐为完全二叉树
2. 链表存储
结点

|左孩子|数据|右孩子|
|---|---|---|
|left|data|right|

```C
typedef Struct TNode{
    int data;
    Struct TNode left;
    Struct TNode right;
}
```
## 二叉树的遍历
- 先序遍历
```C
void PreOrderTraversal(BinTree T)
{
    if(T)
    {
        printf("%d",BT->data);
        PreOrderTraversal(T->left);
        PreOrderTraversal(T->right);
    }
}
```
- 中序遍历
```C
void InOrderTraversal(BinTree T)
{
    if(T)
    {
        PreOrderTraversal(T->left);
        printf("%d",BT->data);
        PreOrderTraversal(T->right);
    }
}
```
- 后序遍历
```C
void InOrderTraversal(BinTree T)
{
    if(T)
    {
        PreOrderTraversal(T->left);
        PreOrderTraversal(T->right);
        printf("%d",BT->data);
    }
}
```
**必须要有中序遍历序列才能确定二叉树**

## 先序和中序遍历确定二叉树
- 根据先序遍历序列第一个结点确定根节点
- 根据根结点在中序遍历序列中分割出左右两个序列
- 对左子树和右子树分别递归使用相同方法进行分解


## 二叉搜索树
其左子树（left subtree）下的每个后代节点（descendant node）的值都小于节点 n 的值；
其右子树（right subtree）下的每个后代节点的值都大于节点 n 的值。
- 查找某个元素
查找效率决定于树的高度
```C
Status Find(int x,BinTree T)
{
    while(T)
    {
        if(x>T->data)
            T = T->right;
        else if(x<T->data)
            T = T->left;
        else
            return T;
    }
    return NULL;
}
```
- 查找最大值
```C
Status FindMax(BinTree T)
{
    if(T) 
        while(T->right)
            T = T->right;
    return T;
}
```
- 二叉搜索树插入
```C
Status Insert(int x,Bintree T)
{
    if(!T)
    {
        T = malloc(sizeof(struct TreeNode));
        T->data = x;
        T->left = T->right = NULL;
    }
    else if(x<T->data)
        T->left = Insert(x,T->Left);
    else if(x>T->data)
        T->right = Insert(x,T->right);
    return T;
}
```
- 二叉搜索树的删除
找到该结点的位置，找到左子树最大值或右子树的最小值
```C
Status Delete(int x,BinTree T)
{
    int temp;
    if(!T) printf("NOT FOUND!");
    else if(x < T->data)
            T->left = Delete(x,T->left);
    else if(x > T->data)
            T->right = Delete(x,T->right);
    else    //找到要删除的结点
        if（T->left && T->right）
        {
            temp = Findmin(T->right);
            T->data = temp->data;
            T->right = Delete(T->data,T->right);
        }
        else
        {
            temp = T;
            if(!T->right)
                T = T->right;
            else if(!T->right)
                T = T->left
            tree(temp);
        }
    return T;
}
```

## 平衡二叉树（是一种搜索树）
AVL树：任一结点左右子树高度差的绝对值不超过1
高度为h的平衡二叉树的最小结点数满足斐波那契数列
RR LL LR RL


