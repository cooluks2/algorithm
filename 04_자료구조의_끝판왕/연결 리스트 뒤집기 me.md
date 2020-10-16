## 연결 리스트 뒤집기

단순 연결리스트의 head 노드가 입력으로 주어진다고 합시다.

이때 이 연결 리스트를 순회하면서 순서를 뒤집어서, 뒤집힌 연결 리스트의 head 노드를 반환하는 함수를 구현 해 봅시다.

예를 들어서, 연결리스트 `2->8->19->37->4->5` 가 주어졌다면 `5->4->37->19->8->2` 를 반환해야 합니다.

1.  이 함수는 Node 객체를 입력으로 받는다는 것에 유의하세요.
2.  배열로 변환 한 후, 뒤집고, 다시 새로운 연결 리스트를 만드는 것도 하나의 방법입니다. 하지만 더 (공간적으로)효율적인 구현법을 생각 해 보세요. 주어진 연결 리스트의 노드들을 그대로 사용하는 방식을 고려 해 보면 됩니다.

<br>

내 풀이

```python

# 실습 3-3과 정의가 약간 바뀌었습니다. 유의하세요.
# 연결 리스트의 노드. 단일 연결 리스트의 경우입니다.
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None
        
    def __str__(self):
        return str(self.val)

# 연결 리스트 클래스. head 와 tail을 가지고 있으며, 가장 뒤에 새로운 노드를 추가하는 addToEnd 함수가 있습니다.
class LinkedList:
    def __init__(self, head):
        self.head = head
        self.tail = head
    
    def addToEnd(self, node):
        self.tail.next = node
        self.tail = node

# head node가 주어졌을 때 해당 링크드리스트를 문자열로 변환해 주는 함수입니다.
def linkedListToStr(node):
    toPrint = []
    while node:
        toPrint.append(str(node.val))
        node = node.next
    return "->".join(toPrint)


# 주어진 배열을 linkedlist로 변환해서 돌려줍니다. 실습 3-1을 참조하세요
def toLinkedList(lst):
    ll = LinkedList(Node(lst[0]))
    for i in range(1, len(lst)):
        ll.addToEnd(Node(lst[i]))
    
    return ll
    
####################################################################################################################################

# head 노드가 주어졌을 때, 해당 링크드 리스트를 뒤집은 후 뒤집힌 링크드 리스트의 헤드를 반환하는 함수를 구현 해 보세요.
def reverseLinkedList(head):
    new_head = head
    temp = None
    
    while new_head:
        new_temp = temp
        temp = new_head
        new_head = new_head.next
        temp.next = new_temp
    return temp

def main():
    nums = [2,8,19,37,4,5]
    head_node = toLinkedList(nums).head
    
    print(linkedListToStr(head_node)) # 2->8->37->4->5
    reversed_head_node = reverseLinkedList(head_node)
    print(linkedListToStr(reversed_head_node)) # 5->4->37->19->8->2

if __name__ == "__main__":
    main()
```

<br>

해설

```python
def reverseLinkedList(head):
    new_head = head # head가 마지막 노드로 바뀌어야 하므로 임시 저장
    temp = None # 마지막 노드 생성
    
    while new_head: # 기존 노드 순회
        new_temp = temp # next에 이용하기 위해 임시 저장
        temp = new_head # 처음 노드를 앞에 붙임
        new_head = new_head.next # head를 바꿔준다.
        temp.next = new_temp # 임시 저장한 temp를 next로 넘겨줌
    return temp
```

