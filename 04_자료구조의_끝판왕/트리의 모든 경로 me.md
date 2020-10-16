## 트리의 모든 경로

완벽한 이진 트리가 주어졌다고 합시다. 이때, 이 트리의 루트(root)에서부터 잎(leaf)까지의 가능한 모든 경로들을 반환하는 함수를 구현 해 봅시다.

가능한 경로상의 value들을 순서대로 포함한 배열들의 배열을 반환하면 됩니다.

예를 들어서,

```
 1
2 3
```

과 같은 트리가 주어졌을 경우, [[1,2], [1,3]] 을 반환하면 되고,

```
   1
 2   3
4 5 6  7
```

과 같은 트리가 주어졌을 경우에는, [[1,2,4], [1,2,5], [1,3,6], [1,3,7]] 을 반환하면 됩니다.

-   깊이 우선 탐색을 활용 해 봅시다.

<br>

내 풀이

```python

#====이 문제를 풀기 위해 필요한 클래스와 함수들입니다. 따로 수정 할 필요는 없습니다.
class Node():
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

def listToCompleteBinaryTree(lst):
    def helper(index):
        if index >= len(lst):
            return None
        node = Node(lst[index])
        node.left = helper(index * 2 + 1)
        node.right = helper(index * 2 + 2)
        return node
    return helper(0)

def printTree(node):
    q = [Node(-1), node]

    line = []
    while q:
        node = q.pop()
        if not node:
            continue
        elif node.val == -1:
            if len(line) > 0:
                print(" ".join(line))
                line = []
                q.insert(0,Node(-1))
        else:
            q.insert(0,node.left)
            q.insert(0,node.right)
            line.append(str(node.val))
#=================================================================================
def all_paths(node):
    all_paths = []
    def dfsHelper(node, cur_path):
        # 여기에 깊이 우선 탐색을 구현 해 봅시다.
        if node.left is None and node.right is None:
            all_paths.append(cur_path + [node.val])
            return
        else:
            dfsHelper(node.left, cur_path + [node.val])
            dfsHelper(node.right, cur_path + [node.val])
        
    dfsHelper(node, [])
    return all_paths
    
def main():
    node = listToCompleteBinaryTree([1,2,3,4,5,6,7])
    printTree(node)
    print(all_paths(node))

if __name__ == "__main__":
    main()
```



