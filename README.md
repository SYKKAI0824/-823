# 11124206施彥愷

## python实现最小堆（Min-Heap）算法
Min-Heap 是一个完整的二叉树，其中每个内部节点中的值小于或等于该节点子节点中的值。

最小堆是一种专用的基于树的数据结构，它满足堆属性。在最小堆中，对于任何给定节点 I，I 的值小于或等于其子节点的值。这可确保最小的元素位于堆的根目录下。

将堆的元素映射到数组中是微不足道的：如果一个节点存储在索引 k 处，则其左子节点存储在索引 2k + 1 处，右侧子节点存储在索引 2k + 2 处，用于基于 0 的索引，对于基于 1 的索引，左侧子节点位于 2k，右侧子节点位于 2k + 1。


![image](https://github.com/user-attachments/assets/84de9d75-f75c-4dc2-9546-580d78950e49)

Min Heap 是如何表示的？
最小堆是一个完整的二叉树。Min 堆通常表示为数组。根元素将位于 Arr[0]。对于任何 i 个节点，即 Arr[i]：

+ Arr[（i -1） / 2] 返回其父节点。
- Arr[（2 * i） + 1] 返回其左子节点。
* Arr[（2 * i） + 2] 返回其右侧子节点。
最小堆上的操作：

1.getMin（）：返回 Min Heap 的根元素。此操作的时间复杂度为 O（1）。

2.extractMin（）：从 MinHeap 中删除最小元素。此操作的时间复杂度为 O（Log n），因为此操作需要在删除 root 后维护堆属性（通过调用 heapify（））。

3.insert（）：插入新键需要 O（Log n） 时间。我们在树的末尾添加一个新键。如果新密钥大于其父密钥，则我们不需要执行任何操作。否则，我们需要遍历以修复违反的堆属性。

以下是 Python 中 Min Heap 的实现 –




  ```
# Python3 implementation of Min Heap 
 import sys

class MinHeap:
    def __init__(self, maxsize):
        self.maxsize = maxsize
        self.size = 0
        self.Heap = [0] * (self.maxsize + 1)
        self.Heap[0] = -1 * sys.maxsize
        self.FRONT = 1

    # Function to return the position of parent for the node currently at pos 
    def parent(self, pos):
        return pos // 2

    # Function to return the position of the left child for the node currently at pos 
    def leftChild(self, pos):
        return 2 * pos

    # Function to return the position of the right child for the node currently at pos 
    def rightChild(self, pos):
        return (2 * pos) + 1

    # Function that returns true if the passed node is a leaf node 
    def isLeaf(self, pos):
        return pos * 2 > self.size

    # Function to swap two nodes of the heap 
    def swap(self, fpos, spos):
        self.Heap[fpos], self.Heap[spos] = self.Heap[spos], self.Heap[fpos]

    # Function to heapify the node at pos 
    def minHeapify(self, pos):
        if not self.isLeaf(pos):
            if (self.Heap[pos] > self.Heap[self.leftChild(pos)] or
                self.Heap[pos] > self.Heap[self.rightChild(pos)]):

                # Swap with the left child and heapify the left child 
                if self.Heap[self.leftChild(pos)] < self.Heap[self.rightChild(pos)]:
                    self.swap(pos, self.leftChild(pos))
                    self.minHeapify(self.leftChild(pos))

                # Swap with the right child and heapify the right child 
                else:
                    self.swap(pos, self.rightChild(pos))
                    self.minHeapify(self.rightChild(pos))

    # Function to insert a node into the heap 
    def insert(self, element):
        if self.size >= self.maxsize:
            return
        self.size += 1
        self.Heap[self.size] = element

        current = self.size

        while self.Heap[current] < self.Heap[self.parent(current)]:
            self.swap(current, self.parent(current))
            current = self.parent(current)

    # Function to print the contents of the heap 
    def Print(self):
        for i in range(1, (self.size // 2) + 1):
            print(" PARENT : " + str(self.Heap[i]) + " LEFT CHILD : " +
                  str(self.Heap[2 * i]) + " RIGHT CHILD : " +
                  str(self.Heap[2 * i + 1]))

    # Function to build the min heap using the minHeapify function 
    def minHeap(self):
        for pos in range(self.size // 2, 0, -1):
            self.minHeapify(pos)

    # Function to remove and return the minimum element from the heap 
    def remove(self):
        popped = self.Heap[self.FRONT]
        self.Heap[self.FRONT] = self.Heap[self.size]
        self.size -= 1
        self.minHeapify(self.FRONT)
        return popped

# Driver Code 
if __name__ == "__main__":
    print('The minHeap is ')
    minHeap = MinHeap(15)
    minHeap.insert(5)
    minHeap.insert(3)
    minHeap.insert(17)
    minHeap.insert(10)
    minHeap.insert(84)
    minHeap.insert(19)
    minHeap.insert(6)
    minHeap.insert(22)
    minHeap.insert(9)
    minHeap.minHeap()

    minHeap.Print()
    print("The Min val is " + str(minHeap.remove()))

```
# 輸出
![image](https://github.com/user-attachments/assets/0db4706b-ace9-4953-b769-e2785a5453ac)

# 使用 Library 函数：

我们使用 heapq 类在 Python 中实现 Heaps。默认情况下，最小堆由此类实现。
```
# Python3 program to demonstrate working of heapq 

from heapq import heapify, heappush, heappop 

# Creating empty heap 
heap = [] 
heapify(heap) 

# Adding items to the heap using heappush function 
heappush(heap, 10) 
heappush(heap, 30) 
heappush(heap, 20) 
heappush(heap, 400) 

# printing the value of minimum element 
print("Head value of heap : "+str(heap[0])) 

# printing the elements of the heap 
print("The heap elements : ") 
for i in heap: 
 print(i, end = ' ') 
print("\n") 

element = heappop(heap) 

# printing the elements of the heap 
print("The heap elements : ") 
for i in heap: 
 print(i, end = ' ')
```
# 輸出
![image](https://github.com/user-attachments/assets/20876e17-cdab-4bbd-aac7-a0b9322c20f9)
