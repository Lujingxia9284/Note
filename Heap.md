# 堆
- 优先队列：特殊的的队列，取出元素顺序按照元素优先权的大小，二不是元素进入队列的先后顺序
- 数组实现：插入总是在尾部
- 链表实现：插入总是在头部
有序数组&有序链表：插入———找到合适位置，删除————删除最后一个元素/删除首元素或最后元素
- 优先队列的**完全二叉树**表示
  结构性：用数组表示完全二叉树
  有序性：任一结点的关键字是其子树所有结点的最大值(或最小值)最大堆/最小堆

# 最大堆的操作
- 创建

|Element|Size|Capasity|
|---|---|---|
|存储元素的数组|元素当前个数|堆的最大容量|

```C
typedef struct HeapStruct{
    int  *Element; //数组
    int Size;
    int Capasity;
}*MaxHeap;
```
创建容量为MaxSize的最大堆
```C
Status Creat(int MaxSize)
{
    MaxHeap H = malloc(sizeof(HeapStruct));  //???
    H->Element = malloc((MaxSize+1)*sizeof(int)); //maxsize+1 是由于从0开始
    H->size = 0;
    H->Capacity = MaxSize;
    H->Element[0] = MaxData; //哨兵
    return H;
}
```
向堆中入新元素，不破坏完全二叉树和有序性
```C
void Insert(MaxHeap H,int item)
{
    int i;
    if(IsFull(H)){
        printf("Heap is Full");
        return;
    }
    i = ++H->Size;  //i指向插入堆中最后一个元素的位置
    for(; H->Element[i/2] < item; i/=2)//插入结点小于父结点
        H->Element[i] = H->Element[i/2];
    H->Element[i]=item; 
}
```










