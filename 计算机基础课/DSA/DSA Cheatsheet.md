# **DSA Cheatsheet**

#### 1.欧几里得算法

如果m能被n整除，那么它们的最大公因数就是n。然而，如果m不能被n整除，那么结果是n与m除以n的余数的最大公因数。

```python
def gcd(m,n):
    while m%n != 0:
        oldm = m
        oldn = n

        m = oldn
        n = oldm%oldn
    return n

print(gcd(20,10))
```

#### 2.binary search + greedy二分

这类问题通常涉及求解==最小化最大值（minMax）或最大化最小值（maxMin）==。遇到此类问题时，应考虑使用二分查找配合贪心策略来进行判定。

08210 河中跳房子  04135 月度开销  LC1760 袋子里最少数目的球

#### 3.Information Retrieval中的倒排索引

从文档到标记的映射被称为**正排索引**，而从标记指向包含该标记的文档（例如：标记 -> 文档_i, 文档_j, ...）的映射则被称为**倒排索引**。

#### 4.Big-O

渐近符号是一种数学工具，它根据==输入大小==计算所需时间，并不需要实际执行代码。

- **大O符号 (Ο)** – 大O符号特别描述了==最坏情况下==的情形。$\Theta$记号渐进地给出算法的平均复杂度，即一个函数的上界和下界。当只有一个渐进上界时，即当n足够大时，使用 O 记号。（同数分中有界量O）
- **欧米伽符号 (Ω)** – 欧米伽(Ω)符号特别描述了最好情况下的情形。
- **西塔符号 (Θ)** – 这个符号代表了算法的平均复杂度。

#### 5.回文串

#### 6.Huffman编码

首先定义了一个 `Node` 类来表示哈夫曼树的节点。然后，使用最小堆来构建哈夫曼树，每次从堆中取出两个频率最小的节点进行合并，直到堆中只剩下一个节点，即哈夫曼树的根节点。接着，使用递归方法计算哈夫曼树的带权外部路径长度（weighted external path length）。最后，输出计算得到的带权外部路径长度。

#### 7.二叉搜索树

·平衡二叉搜索树节点个数：

当高度为h时，$N_h = 1 + N_{h-1} + N_{h-2}$

·左右旋操作：

![image-20250420111041005](/Users/luc/Library/Application Support/typora-user-images/image-20250420111041005.png)

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
        self.height = 1

class AVL:
    def __init__(self):
        self.root = None
def insert(self, value):
    if not self.root:
        self.root = Node(value)
    else:
        self.root = self._insert(value, self.root)

def _insert(self, value, node):
    if not node:
        return Node(value)
    elif value < node.value:
        node.left = self._insert(value, node.left)
    else:
        node.right = self._insert(value, node.right)

    node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))

    balance = self._get_balance(node)

    if balance > 1:
        if value < node.left.value:	# 树形是 LL
            return self._rotate_right(node)
        else:	# 树形是 LR
            node.left = self._rotate_left(node.left)
            return self._rotate_right(node)

    if balance < -1:
        if value > node.right.value:	# 树形是 RR
            return self._rotate_left(node)
        else:	# 树形是 RL
            node.right = self._rotate_right(node.right)
            return self._rotate_left(node)

    return node

def _get_height(self, node):
    if not node:
        return 0
    return node.height

def _get_balance(self, node):
    if not node:
        return 0
    return self._get_height(node.left) - self._get_height(node.right)

def _rotate_left(self, z):
    y = z.right
    T2 = y.left
    y.left = z
    z.right = T2
    z.height = 1 + max(self._get_height(z.left), self._get_height(z.right))
    y.height = 1 + max(self._get_height(y.left), self._get_height(y.right))
    return y

def _rotate_right(self, y):
    x = y.left
    T2 = x.right
    x.right = y
    y.left = T2
    y.height = 1 + max(self._get_height(y.left), self._get_height(y.right))
    x.height = 1 + max(self._get_height(x.left), self._get_height(x.right))
    return x

def preorder(self):
    return self._preorder(self.root)

def _preorder(self, node):
    if not node:
        return []
    return [node.value] + self._preorder(node.left) + self._preorder(node.right)
n = int(input().strip())
sequence = list(map(int, input().strip().split()))

avl = AVL()
for value in sequence:
    avl.insert(value)

print(' '.join(map(str, avl.preorder())))
```

#### 8.堆

```python
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0
def percUp(self, i):
    while i // 2 > 0:
        if self.heapList[i] < self.heapList[i // 2]:
            tmp = self.heapList[i // 2]
            self.heapList[i // 2] = self.heapList[i]
            self.heapList[i] = tmp
        i = i // 2

def insert(self, k):
    self.heapList.append(k)
    self.currentSize = self.currentSize + 1
    self.percUp(self.currentSize)

def percDown(self, i):
    while (i * 2) <= self.currentSize:
        mc = self.minChild(i)
        if self.heapList[i] > self.heapList[mc]:
            tmp = self.heapList[i]
            self.heapList[i] = self.heapList[mc]
            self.heapList[mc] = tmp
        i = mc

def minChild(self, i):
    if i * 2 + 1 > self.currentSize:
        return i * 2
    else:
        if self.heapList[i * 2] < self.heapList[i * 2 + 1]:
            return i * 2
        else:
            return i * 2 + 1

def delMin(self):
    retval = self.heapList[1]
    self.heapList[1] = self.heapList[self.currentSize]
    self.currentSize = self.currentSize - 1
    self.heapList.pop()
    self.percDown(1)
    return retval

def buildHeap(self, alist):
    i = len(alist) // 2
    self.currentSize = len(alist)
    self.heapList = [0] + alist[:]
    while (i > 0):
        print(f'i = {i}, {self.heapList}')
        self.percDown(i)
        i = i - 1
    print(f'i = {i}, {self.heapList}')``
```

#### 9.图

**vertex类**

```python
class Vertex:
    def __init__(self, key):
        self.key = key
        self.neighbors = {}
def get_neighbor(self, other):
    return self.neighbors.get(other, None)

def set_neighbor(self, other, weight=0):
    self.neighbors[other] = weight

def __repr__(self):  # 为开发者提供调试信息
    return f"Vertex({self.key})"

def __str__(self):  # 面向用户的输出
    return (
            str(self.key)
            + " connected to: "
            + str([x.key for x in self.neighbors])
    )

def get_neighbors(self):
    return self.neighbors.keys()

def get_key(self):
    return self.key`
```

**graph类**

```python
class Graph:
    def __init__(self):
        self.vertices = {}
def set_vertex(self, key):
    self.vertices[key] = Vertex(key)

def get_vertex(self, key):
    return self.vertices.get(key, None)

def __contains__(self, key):
    return key in self.vertices

def add_edge(self, from_vert, to_vert, weight=0):
    if from_vert not in self.vertices:
        self.set_vertex(from_vert)
    if to_vert not in self.vertices:
        self.set_vertex(to_vert)
    self.vertices[from_vert].set_neighbor(self.vertices[to_vert], weight)

def get_vertices(self):
    return self.vertices.keys()

def __iter__(self):
    return iter(self.vertices.values())
```

**‼️骑士周游**

```python
import sys

def is_valid_move(x, y, board, n):
    return 0 <= x < n and 0 <= y < n and board[x][y] == -1

def get_degree(x, y, board, n, moves):
    count = 0
    for dx, dy in moves:
        if is_valid_move(x + dx, y + dy, board, n):#注意统计degree时访问过的节点不计入！！！
            count += 1
    return count

def knights_tour_warnsdorff(n, sr, sc):
    moves = [(2, 1), (1, 2), (-1, 2), (-2, 1),
             (-2, -1), (-1, -2), (1, -2), (2, -1)]
    board = [[-1 for _ in range(n)] for _ in range(n)]
    board[sr][sc] = 0
    
    def backtrack(x, y, move_count):
        if move_count == n * n:
            return True
        
        next_moves = []
        for dx, dy in moves:
            nx, ny = x + dx, y + dy
            if is_valid_move(nx, ny, board, n):
                degree = get_degree(nx, ny, board, n, moves)
                next_moves.append((degree, nx, ny))
        
        next_moves.sort()  # 按 Warnsdorff 规则选择最少可行移动的方向
        
        for _, nx, ny in next_moves:
            board[nx][ny] = move_count
            if backtrack(nx, ny, move_count + 1):
                return True
            board[nx][ny] = -1  # 回溯
        
        return False
    
    if backtrack(sr, sc, 1):
        print("success")
    else:
        print("fail")

if __name__ == "__main__":
    n = int(sys.stdin.readline().strip())
    sr, sc = map(int, sys.stdin.readline().strip().split())
    knights_tour_warnsdorff(n, sr, sc)
```



## 关于 kmp 算法中 next 数组的周期性质

**🌟 引理：**

对于某一字符串 $S[1∼i]$，在它的 `next[i]` 的候选值中，若存在某一 `next[i]` 使得：

> 注意这个i是从1开始的，写代码通常从0开始。

$i \mod  (i−next[i])=0$

那么：

- $S[1∼(i−next[i])]$ 是 $S[1∼i]$ 的**最小循环元**（最小周期子串）；
- $K= \frac{i}{i−next[i]}$ 是这个循环元在 $S[1∼i]$ 中出现的次数。

------

这个引理揭示了 KMP 算法中 `next` 数组与字符串的**周期性质**之间的联系，是字符串处理中的一个经典思想。我们来详细解释它的含义与推导过程。

🧠 **解释与推导**

KMP 算法中 `next[i]` 表示：在 $S[1∼i]$ 中，最长的**真前缀 = 真后缀**的长度。

设：

- $p=i−next[i]$

也就是说，当前字符串 $S[1∼i]$ 的最长相等前后缀长度是 $next[i]$，剩下的部分（中间不能匹配的部分）长度为 p。

如果 $i \mod  p=0$，也就是 i 是 p 的整数倍，意味着我们可以将长度为 p 的子串重复 $K = \frac{i}{p}$ 次，刚好构成整个 $S[1∼i]$。

这说明：

- S[1∼i] 是由某个长度为 p 的子串重复 K 次构成；
- 即 S[1∼p] 是 S[1∼i] 的**最小循环节（最小周期）**；
- K 是循环次数。

------

✅ **举个例子**

考虑字符串 `ababab`，即 S=a b a b a b

构造其 `next` 数组：

| i    | S[i] | next[i] |
| ---- | ---- | ------- |
| 1    | a    | 0       |
| 2    | b    | 0       |
| 3    | a    | 1       |
| 4    | b    | 2       |
| 5    | a    | 3       |
| 6    | b    | 4       |

对 i=6，有 next[6] = 4，则：

- p = i−next[i] = 6−4=2
- i mod  p = 6 mod  2=0，满足条件
- 所以 `ab`（即 S[1∼2]）是 `ababab` 的最小循环元；
- $K=\frac62=3$，循环了 3 次。

------

🔁 用途：判断字符串是否由某个子串重复构成

基于这个引理，可以用来快速判断一个字符串是否可以由某个子串重复得到。例如：

```python
def is_repeated_pattern(s: str) -> bool:
    n = len(s)
    next = [0] * (n + 1)
    j = 0
    for i in range(2, n + 1):
        while j > 0 and s[j] != s[i-1]:
            j = next[j]
        if s[j] == s[i - 1]:
            j += 1
        next[i] = j

    p = n - next[n]
    return n % p == 0 and n != p

print(is_repeated_pattern("ababab"))  # True
```

------

📌 总结

引理中的结论可以归纳如下：

> 如果一个字符串 $S[1∼i]$ 的 `next[i]` 满足 $i \mod  (i−next[i])==0$，
> 则 $S[1∼(i−next[i])]$ 是它的最小循环节，
> 且重复次数为 $K= \frac{i}{i−next[i]}$。

这种性质在字符串压缩、周期检测、重复匹配等应用中非常重要。







#### ==***小细节**==

1.`tail,slow.next,slow=slow,tail,slow.next`

从左到右赋值（最好分开写）

2.bfs标记应在访问前![image-20250510174919991](/Users/luc/Library/Application Support/typora-user-images/image-20250510174919991.png)

3.dfs的退回啊啊啊啊啊啊啊

4.Vertex类+heap：定义__lt__
