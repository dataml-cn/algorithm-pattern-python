# 二叉树

## 知识点

### 二叉树遍历

二叉树的遍历方式，以访问根节点的顺序不同，有3种分别为：

- **前序遍历**：**根节点** --> 左子树  --> 右子树
- **中序遍历**：左子树 --> **根节点** --> 右子树
- **后序遍历**：左子树 --> 右子树 --> **根节点**

> 左子树都是优先右子树

在解释具体的遍历方式前，我们先定义树的结构
```python
class TreeNode:
    def __init__(self, val, left: TreeNode, right: TreeNode):
        self.val = val
        self.left = left
        self.right = right
```


#### 前序递归

```python
def pre_order_traversal(root: TreeNode):
    if root == null:
        return
    
    # 根节点 --> 左子树  --> 右子树
    print(root.val)
    preorder_traversal(root.left)
    preorder_traversal(root.right)
```

#### 前序非递归

```python

def pre_order_traversal(root: TreeNode) -> list[int]:

    if not root:
        return None

    result = list()
    stack = list()

    while True:
        while True:
            result.append(root.val)
            stack.append(root)
            
            if root.left:
                root = root.left
            else:
                break
        node = result.pop()

        if node.right:
            root = node.right
        else:
            break
    }

    return result
```

#### 中序非递归

```python
def in_order_traversal(root: TreeNode) -> list[int]:

    result = []
    stack = []

    if root is None:
        return result

    while stack or root:

        while root:
            stack.append(root)
            root = root.left
        
        root = stack.pop()
        result.append(root.val)
    
        root = root.right
    
    return result
```

#### 后序非递归

```python
def post_order_traversal(root: TreeNode) -> list[int]: 

    stack = []
    result = []

    last_visit = None
    
    if root is None:
        return result

    while stack or root:

        while root:
            stack.append(root)
            root = root.left
        
        node = stack[-1]
        if node.right is None or node.right == last_visit:
            node = stack.pop()
            result.append(root.val)
            last_visit = node
        else:
            root = node.right

	return result
}
```

> 核心：根节点必须在右节点弹出之后，再弹出

#### DFS 深度搜索-从上到下

```python

def pre_order_traversal(root: TreeNode) -> list[int]:
    result = []
    dfs(root, result)
    return result


def dfs(root: TreeNode, result: list[int]) {
    if root is None:
        return

    result = result.append(root.val)
    dfs(root.left, result)
    dfs(root.right, result)
}
```

#### DFS 深度搜索-从下向上（分治法）

```python
def pre_order_traversal(root: TreeNode) -> list[int]:
    result = divide_and_conquer(root)
    return result


def divide_and_conquer(root: TreeNode) -> list[int]:
    result = []

    if root is None:
        return result
    
    # divide
    left_result = divide_and_conquer(root.left)
    right_result = divide_and_conquer(root.right)

    # conquer
    result.append(root.val)
    result.extend(left_result)
    result.extend(right_result)

    return result
```

> DFS 两种实现方式区别
> - 从上到下, 一般将最终结果通过指针**参数**传入
> - 分治法, 一般递归返回**结果最后合并**

#### BFS 层次遍历

```python
def level_order(root: TreeNode) -> list[int]:
    
    result = []
    if root is None: 
        return result
    
    queue = [root]
    
    while len(queue) > 0:

        level_values = []
        level_len = len(queue)

        for i in range(level_len):

            node = queue.pop()
            level_values.append(node.val)

            if node.left:
                queue.append(node.left)
            if level.right:
                queue.append(node.right)
        
        result.extend(level_values)

    return result
```

### 分治法应用

先分别处理局部，再合并结果

适用场景

- 快速排序
- 归并排序
- 二叉树相关问题

分治法模板

- 递归返回条件
- 分段处理
- 合并结果

```python
def traversal(root: TreeNode) -> ResultType:

    if root is None:
        # do something 
        return result
    else:

        # Divide
        ResultType left = traversal(root.left)
        ResultType right = traversal(root.right)

        # Conquer
        ResultType result = Merge from left and right

        return result
}
```

#### 典型示例

```python
# 通过分治法遍历二叉树

def pre_order_traversal(root: TreeNode) -> list[int]: 
    result = divide_and_conquer(root)
    return result

def divide_and_conquer(root: TreeNode) list[int]: 
    result = []

    if root is None:
        return result

    # Divide
    left_result = divide_and_conquer(root.left)
    right_result = divide_and_conquer(root.right)
    
    # Conquer
    result.append(root.val)
    result.extend(left_result)
    result.extend(right_result)

    return result
}
```

#### 归并排序  

```python
def merge(nums: list[int]) -> list[int]:
    return merge_sort(nums)

def merge_sort(nums: list[int]) -> list[int]: 
    
    if len(nums) <= 1:
        return nums
    
    # 分治法：divide 分为两段
    mid = len(nums) // 2
    left = merge_sort(nums[:mid])
    right = merge_sort(nums[mid:])
    
    # 合并两段数据
    result = merge_ordered_arrays(left, right)
    return result

def merge_ordered_arrays(left: list[int], right: list[int]) -> list[int]:

    while left and right:

        if left[0] > right[0] {
            result.append(right.pop())
        } else {
            result.append(left.pop())
        }
    }
    
    # 剩余部分合并
    result.extend(left)
    result.extend(right)
    return
}
```

> 递归需要返回结果用于合并

#### 快速排序  

```python
def quick_sort(nums list[int]) -> list[int]:

	# 思路：把一个数组分为左右两段，左段小于右段，类似分治法没有合并过程
	quick_sort_detail(nums, 0, len(nums)-1)
	return nums



def quick_sort_detail(nums: list[int], start: int, end: int):
    # 原地交换，传入开始、结束交换索引范围

	if start < end:
        # 分治法：divide
		pivot = partition(nums, start, end)
		quick_sort_detail(nums, 0, pivot-1)
		quick_sort_detail(nums, pivot+1, end)

def partition(nums list[int], start: int, end: int) -> int:
	p = nums[end]
	
    # i: 下标小于等于 i 的部分都小于 p, 下标 i+1 对应元素大于等于 p 
    # j: 目的是找到下一个小于 p 的元素, 交换(i+1, j)使得, 下标小于等于i+1的部分都小于p
    
    i = start - 1
    for j in range(end):
        if nums[j] < p:
            i = i + 1
            swap(nums, i, j)

    i = i + 1
    swap(nums, i + 1, end)

	return i


def swap(nums: list[int], i: int, j: int):
	t = nums[i]
	nums[i] = nums[j]
	nums[j] = t

```

> 快排由于是原地交换所以没有合并过程
> 传入的索引是存在的索引（如：0、length-1 等），越界可能导致崩溃
> 核心进行partition, 分成左右两部分

常见题目示例

#### [maximum-depth-of-binary-tree](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

> 给定一个二叉树，找出其最大深度。

**思路**

- 分治法
  - 左边深度
  - 右边深度
  - 左右深度最大值 + 1

```python
# CPU: 56ms, 33.09%, MEMARY:16.5M, 62.92% 
class Solution:
    def maxDepth(self, root: TreeNode) -> int:

        if not root or root.val is None:
            return 0
        else:
            left_depth = self.maxDepth(root.left) if root.left else 0
            right_depth = self.maxDepth(root.right) if root.right else 0

            return max(left_depth, right_depth) + 1
```

#### [balanced-binary-tree](https://leetcode-cn.com/problems/balanced-binary-tree/)

> 给定一个二叉树，判断它是否是高度平衡的二叉树。
> 
> 高度平衡的二叉树: 一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。

**思路**  

- 分治法, 需要同时满足以下条件
  - 左边高度平衡
  - 右边高度平衡
  - 左右两边高度 <= 1  
- 需要返回是否平衡及高度（二义性：一个变量有两种含义）
  - -1: 不平衡
  - \> 0: 树高度

```python
# CPU: 48ms, 98.34%, MEMARY:18.6M, 83.51% 
class Solution:

    def isBalanced(self, root: TreeNode) -> bool:
        return self.max_depth(root) != -1

    def max_depth(self, root: TreeNode) -> int:

        if root is None:
            return 0
        else:
            left = self.max_depth(root.left)
            right = self.max_depth(root.right)

        if left == -1 or right == -1 or abs(left-right) > 1:
            return -1
        else:
            return left + 1 if left > right else right + 1

```

**注意**

> 一般工程中, 不建议用一个变量表示两种含义

#### [binary-tree-maximum-path-sum](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

> 给定一个**非空**二叉树，返回其最大路径和。  
> 
> **路径** 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。同一个节点在一条路径序列中至多出现一次 。该路径至少包含一个节点，且不一定经过根节点。  
> 
> **路径和** 是路径中各节点值的总和。


**思路**  
分治法，分为三种情况：

1. 左子树最大路径和最大
2. 右子树最大路径和最大
3. 左右子树**最大贡献**加根节点最大
   
需要保存两个变量
- 最大路径和：max_path
  - 不包含, max(左、右最大路径)
  - 包含value, max(左+右节点最大贡献, 左节点最大贡献, 右节点最大贡献, 0) + value

- 当前节点对父节点最大贡献: max_gain
  - 不包含, 0
  - 包含节点, max(左、右节点最大贡献, 0) + value

- 当节点为空时
  - 最大路径应该, **很小的负数**, 不然上层节点值为负时, 最大路径可能选择错误


然后比较这个两个变量选择最大值即可

```python
# CPU: 100ms, 54.72%, MEMARY:21.6M, 91.23% 

class Solution:
    def maxPathSum(self, root: TreeNode) -> int:

        return self.divide(root)[0]


    def divide(self, root: TreeNode) -> tuple:

        # return: max_path, max_gain
        # max_path: 当前子树下的最大路径和
        #           最大路径: 不包含当前节点, 左右子树中的最大路径; 或者包含当前节点, 左右子树有可能贡献
        #           max_path = max(righ_max_path, left_max_path, max(right_gain, left_gain, right_gain + left_gain, 0) + value)
        # max_gain: 当前节点, 作为子节点可以提供的贡献
        #           当前节点的贡献:自身+左右其中之一, 或者贡献为0 
        #           max_gain = max(max(right_gain, left_gain, 0) + value, 0)

        if root is None: 
            return -(1 << 31), 0
        else:

            left_max_path, left_max_gain = self.divide(root.left)
            right_max_path, right_max_gain = self.divide(root.right)

            max_gain = max(max(left_max_gain, right_max_gain, 0) + root.val, 0)
            max_path = max(max(left_max_path, right_max_path), max(left_max_gain, right_max_gain, left_max_gain + right_max_gain, 0) + root.val)

            return max_path, max_gain
```

#### lowest-common-ancestor-of-a-binary-tree

[lowest-common-ancestor-of-a-binary-tree](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

> 给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

思路：分治法，有左子树的公共祖先或者有右子树的公共祖先，就返回子树的祖先，否则返回根节点

```go
func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
    // check
    if root == nil {
        return root
    }
    // 相等 直接返回root节点即可
    if root == p || root == q {
        return root
    }
    // Divide
    left := lowestCommonAncestor(root.Left, p, q)
    right := lowestCommonAncestor(root.Right, p, q)


    // Conquer
    // 左右两边都不为空，则根节点为祖先
    if left != nil && right != nil {
        return root
    }
    if left != nil {
        return left
    }
    if right != nil {
        return right
    }
    return nil
}
```

### BFS 层次应用

#### binary-tree-level-order-traversal

[binary-tree-level-order-traversal](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

> 给你一个二叉树，请你返回其按  **层序遍历**  得到的节点值。 （即逐层地，从左到右访问所有节点）

思路：用一个队列记录一层的元素，然后扫描这一层元素添加下一层元素到队列（一个数进去出来一次，所以复杂度 O(logN)）

```go
func levelOrder(root *TreeNode) [][]int {
	result := make([][]int, 0)
	if root == nil {
		return result
	}
	queue := make([]*TreeNode, 0)
	queue = append(queue, root)
	for len(queue) > 0 {
		list := make([]int, 0)
        // 为什么要取length？
        // 记录当前层有多少元素（遍历当前层，再添加下一层）
		l := len(queue)
		for i := 0; i < l; i++ {
            // 出队列
			level := queue[0]
			queue = queue[1:]
			list = append(list, level.Val)
			if level.Left != nil {
				queue = append(queue, level.Left)
			}
			if level.Right != nil {
				queue = append(queue, level.Right)
			}
		}
		result = append(result, list)
	}
	return result
}
```

#### binary-tree-level-order-traversal-ii

[binary-tree-level-order-traversal-ii](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

> 给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

思路：在层级遍历的基础上，翻转一下结果即可

```go
func levelOrderBottom(root *TreeNode) [][]int {
    result := levelOrder(root)
    // 翻转结果
    reverse(result)
    return result
}
func reverse(nums [][]int) {
	for i, j := 0, len(nums)-1; i < j; i, j = i+1, j-1 {
		nums[i], nums[j] = nums[j], nums[i]
	}
}
func levelOrder(root *TreeNode) [][]int {
	result := make([][]int, 0)
	if root == nil {
		return result
	}
	queue := make([]*TreeNode, 0)
	queue = append(queue, root)
	for len(queue) > 0 {
		list := make([]int, 0)
        // 为什么要取length？
        // 记录当前层有多少元素（遍历当前层，再添加下一层）
		l := len(queue)
		for i := 0; i < l; i++ {
            // 出队列
			level := queue[0]
			queue = queue[1:]
			list = append(list, level.Val)
			if level.Left != nil {
				queue = append(queue, level.Left)
			}
			if level.Right != nil {
				queue = append(queue, level.Right)
			}
		}
		result = append(result, list)
	}
	return result
}
```

#### binary-tree-zigzag-level-order-traversal

[binary-tree-zigzag-level-order-traversal](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

> 给定一个二叉树，返回其节点值的锯齿形层次遍历。Z 字形遍历

```go
func zigzagLevelOrder(root *TreeNode) [][]int {
	result := make([][]int, 0)
	if root == nil {
		return result
	}
	queue := make([]*TreeNode, 0)
	queue = append(queue, root)
	toggle := false
	for len(queue) > 0 {
		list := make([]int, 0)
		// 记录当前层有多少元素（遍历当前层，再添加下一层）
		l := len(queue)
		for i := 0; i < l; i++ {
			// 出队列
			level := queue[0]
			queue = queue[1:]
			list = append(list, level.Val)
			if level.Left != nil {
				queue = append(queue, level.Left)
			}
			if level.Right != nil {
				queue = append(queue, level.Right)
			}
		}
		if toggle {
			reverse(list)
		}
		result = append(result, list)
		toggle = !toggle
	}
	return result
}
func reverse(nums []int) {
	for i := 0; i < len(nums)/2; i++ {
		nums[i], nums[len(nums)-1-i] = nums[len(nums)-1-i], nums[i]
	}
}
```

### 二叉搜索树应用

#### validate-binary-search-tree

[validate-binary-search-tree](https://leetcode-cn.com/problems/validate-binary-search-tree/)

> 给定一个二叉树，判断其是否是一个有效的二叉搜索树。

思路 1：中序遍历，检查结果列表是否已经有序

思路 2：分治法，判断左 MAX < 根 < 右 MIN

```go
// v1
func isValidBST(root *TreeNode) bool {
    result := make([]int, 0)
    inOrder(root, &result)
    // check order
    for i := 0; i < len(result) - 1; i++{
        if result[i] >= result[i+1] {
            return false
        }
    }
    return true
}

func inOrder(root *TreeNode, result *[]int)  {
    if root == nil{
        return
    }
    inOrder(root.Left, result)
    *result = append(*result, root.Val)
    inOrder(root.Right, result)
}


```

```go
// v2分治法
type ResultType struct {
	IsValid bool
    // 记录左右两边最大最小值，和根节点进行比较
	Max     *TreeNode
	Min     *TreeNode
}

func isValidBST2(root *TreeNode) bool {
	result := helper(root)
	return result.IsValid
}
func helper(root *TreeNode) ResultType {
	result := ResultType{}
	// check
	if root == nil {
		result.IsValid = true
		return result
	}

	left := helper(root.Left)
	right := helper(root.Right)

	if !left.IsValid || !right.IsValid {
		result.IsValid = false
		return result
	}
	if left.Max != nil && left.Max.Val >= root.Val {
		result.IsValid = false
		return result
	}
	if right.Min != nil && right.Min.Val <= root.Val {
		result.IsValid = false
		return result
	}

	result.IsValid = true
    // 如果左边还有更小的3，就用更小的节点，不用4
    //  5
    // / \
    // 1   4
    //      / \
    //     3   6
	result.Min = root
	if left.Min != nil {
		result.Min = left.Min
	}
	result.Max = root
	if right.Max != nil {
		result.Max = right.Max
	}
	return result
}
```

#### insert-into-a-binary-search-tree

[insert-into-a-binary-search-tree](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)

> 给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。

思路：找到最后一个叶子节点满足插入条件即可

```go
// DFS查找插入位置
func insertIntoBST(root *TreeNode, val int) *TreeNode {
    if root == nil {
        root = &TreeNode{Val: val}
        return root
    }
    if root.Val > val {
        root.Left = insertIntoBST(root.Left, val)
    } else {
        root.Right = insertIntoBST(root.Right, val)
    }
    return root
}
```

## 总结

- 掌握二叉树递归与非递归遍历
- 理解 DFS 前序遍历与分治法
- 理解 BFS 层次遍历

## 练习

- [x] [maximum-depth-of-binary-tree](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
- [ ] [balanced-binary-tree](https://leetcode-cn.com/problems/balanced-binary-tree/)
- [ ] [binary-tree-maximum-path-sum](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)
- [ ] [lowest-common-ancestor-of-a-binary-tree](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- [ ] [binary-tree-level-order-traversal](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
- [ ] [binary-tree-level-order-traversal-ii](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)
- [ ] [binary-tree-zigzag-level-order-traversal](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)
- [ ] [validate-binary-search-tree](https://leetcode-cn.com/problems/validate-binary-search-tree/)
- [ ] [insert-into-a-binary-search-tree](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)
