# 심화된 자료구조

### 연결리스트(Linked List)

**연결 리스트란?**

-   여러개의 **노드**들이 한 줄로 연결

-   노드 = **저장할 데이터** + 다음 노드로의 연결

![image-20201012230039454](README.assets/image-20201012230039454.png)  

<br>

**단순 연결 리스트**

-   **한 방향**으로만 이어진 연결 리스트

![image-20201012230045998](README.assets/image-20201012230045998.png)  

<br>

**이중 연결 리스트**

-   **양쪽 방향**으로 이어진 연결 리스트

![image-20201012230105724](README.assets/image-20201012230105724.png)  

<br>

**원형 연결 리스트**

-   **가장 뒤의 노드**가 **맨 앞의 노드**에 연결된 연결 리스트

![image-20201012230116549](README.assets/image-20201012230116549.png)  

<br>

**기타 연결 리스트**

-   **아무 형태**의 연결 리스트 모두 가능!

![image-20201012230129926](README.assets/image-20201012230129926.png)  

<br>

**배열 VS 연결 리스트**

-   **배열**: 인덱스 이용해서 데이터 접근
    ![image-20201012230139772](README.assets/image-20201012230139772.png)  

-   **연결 리스트**: 현재 노드에서 연결된 노드로만

    ![image-20201012230149562](README.assets/image-20201012230149562.png)  

<br>

**헤드 Head**

-   어딘가에서는 시작을 해야하므로!

![image-20201012230204149](README.assets/image-20201012230204149.png)  

<br>

**연결 리스트 시간 복잡도**

-   자료 중간에 추가/삭제 : `O(1)`

![image-20201012230227993](README.assets/image-20201012230227993.png)  

<br>

>   배열 시간 복잡도와 비교해보면?
>
>   nums.insert(3, 9) : `O(N)`

<br>

<br>

[실습 1]

## 연결 리스트 <–> 배열 변환하기

연결 리스트 클래스 LinkedList와, 그 노드 클래스 Node가 주어졌습니다.

연결 리스트 객체가 주어졌을때 이를 배열로 변환해서 반환하는 함수 toArray와, 배열이 주어졌을때 이를 연결 리스트로 변환해서 반환하는 함수 toLinkedList를 구현 해 봅시다.

```python
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
        
    def __str__(self):
        node = self.head
        toPrint = []
        while node:
            toPrint.append(str(node.val))
            node = node.next
        return "->".join(toPrint)

####################################################################################################################################

# 주어진 연결 리스트 ll을 배열로 변환해 봅시다.
# 이때 연결 리스트 LinkedList의 객체가 입력으로 주어진다고 가정합니다.
def toArray(llNode):
    arr = []
    it = llNode.head
    
    while it != llNode.tail: # 마지막에서 두번째 원소까지 순회
        arr.append(it.val)
        it = it.next
        
    arr.append(it.val) # 마지막 원소
    return arr


# 주어진 배열을 연결 리스트로 변환 해 봅시다.
def toLinkedList(lst):
    
    llNode = LinkedList(Node(lst[0]))
    
    for i in lst[1:]:
        llNode.addToEnd(Node(i))
        
    return llNode

def example():
    ## Linkedlist 클래스와 Node 클래스를 사용하는 예시입니다.
    ll = LinkedList(Node(3))
    ll.addToEnd(Node(4))
    ll.addToEnd(Node(8))
    print(ll)
    print(ll.head)
    print(ll.tail)

def main():
    example()
    nums = [2,8,19,37,4,5]
    ll = toLinkedList(nums)
    print(ll)
    lst = toArray(ll)
    print(lst)

if __name__ == "__main__":
    main()
```

<br>

<br>

[실습 2]

## 연결 리스트에서 노드 삭제하기

연결 리스트가 주어지고, 이 연결리스트에서 삭제하고 싶은 노드의 값이 주어졌다고 해 봅시다.

연결 리스트를 순회하면서 해당 노드를 찾아서, 삭제하는 함수를 만들어 봅시다.

주어진 연결 리스트에서 직접 삭제를 시행하면 되기 때문에, 해당 연결 리스트를 반환 할 필요는 없습니다.

<br>

#### 문제 조건

-   연결리스트에는 중복된 수가 없습니다.

<br>

```python
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
        
    def __str__(self):
        node = self.head
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

def deleteNode(ll, valToDelete):
    if ll.head.val == valToDelete:
        ll.head = ll.head.next
    
    curNode = ll.head
    nextNode = curNode.next
    
    while nextNode:
        if nextNode.val == valToDelete:
            curNode.next = nextNode.next # 삭제
            
            if nextNode == ll.tail:
                ll.tail = curNode
            break
            
        curNode = curNode.next
        nextNode = curNode.next
    return None

def main():
    nums = [2,8,19,37,4,5]
    ll = toLinkedList(nums)
    print(ll)
    deleteNode(ll, 19)
    print(ll) # 19를 삭제하였으므로, 2->8->37->4->5
    deleteNode(ll, 3)
    print(ll) # 3이 없으므로, 2->8->37->4->5

if __name__ == "__main__":
    main()
```

<br>

<br>

### 큐(Queue)

**큐**

-   먼저 줄 선 사람이 먼저 나간다
    = FIRST IN FIRST OUT (FIFO)

![image-20201012230322451](README.assets/image-20201012230322451.png)  

<br>

**큐 시간 복잡도**

-   입력하기 : `O(1)`
-   출력하기 : `O(1)`

<br>

**큐 작동 방식**

![image-20201012230348572](README.assets/image-20201012230348572.png)  

<br>

**큐 in Python**

-   queue library 활용

```python
import queue
q = queue.Queue()
q.put(2)
q.put(8)
q.get()
```

<br>

-   배열을 큐(Queue)로 활용

```python
q = [8, 19, 37, 4, 5]

q.insert(0, 2) # 맨 앞에 입력한다
q.pop() # 맨 뒤에서 가져온다
```

>   배열을 활용했을 때 문제점은? 시간 복잡도!

<br>

<br>

[실습 3]

## 스트리밍 데이터의 이동 평균

정수 데이터가 스트리밍으로 (한번에 하나씩) 주어진다고 합시다. 이때, 주어진 범위 만큼의 이동 평균을 구하는 클래스 MovingAvg를 만들어 봅시다.

MovingAvg는 처음에 이동 평균의 범위를 입력받아서 초기화 되며, 매 정수 데이타가 입력되는 nextVal(num)함수는 이때까지의 이동 평균을 반환합니다.

예를 들어서, `2,8,19,37,4,5` 의 순서로 데이터가 입력되고, 이동 평균의 범위는 3이라고 합시다. 이 경우 다음과 같이 MovingAvg가 사용 될 것입니다.

```python
ma = MovingAvg(3)
print(ma.nextVal(2))    
# 현재까지 입력된 값이 2밖에 없으므로, 2를 반환합니다.

print(ma.nextVal(8))    
# 현재까지 입력된 값이 2와 8이므로, (2 + 8) / 2 = 5 를 반환합니다.

print(ma.nextVal(19))   
# (2 + 8 + 19) / 3 = 9.666666666666666 를 반환합니다.

print(ma.nextVal(37))    
# 이동 평균의 범위가 3이므로, 지난 3개의 값의 평균 (8 + 19 + 37) / 3 = 21.333333333333332 을 반환합니다.

print(ma.nextVal(4))    
# (19 + 37 + 4) / 3 = 20 을 반환합니다.

print(ma.nextVal(5))    
# (37 + 4 + 5) / 3 = 15.333333333333334 를 반환합니다.
```

<br>

class 정의

```python
import queue

class MovingAvg():
    def __init__(self, size):
        self.size = size
        self.q = queue.Queue()
        self.sum = 0

    def nextVal(self, num):
        if self.q.qsize() < self.size:
            self.q.put(num)
            self.sum += num
            return self.sum / self.q.qsize()
        else:
            self.sum -= self.q.get()
            self.q.put(num)
            self.sum += num
            return self.sum / self.size

def queueExample():
    q = queue.Queue()
    q.put(1)
    q.put(2)
    print(q.qsize())
    print(q.get())
    print(q.qsize())
    print(q.get())
    
def main():
    queueExample()

    nums = [2,8,19,37,4,5]
    ma = MovingAvg(3)
    results = []
    for num in nums:
        avg = ma.nextVal(num)
        results.append(avg)
    print(results) # [2.0, 5.0, 9.666666666666666, 21.333333333333332, 20.0, 15.333333333333334]
if __name__ == "__main__":
    main()
```

<br>

<br>

### 스택(Stack)

**스택**

-   나중에 줄 선 사람이 먼저 나간다

    = LAST IN FIRST OUT (LIFO)

![image-20201012230418206](README.assets/image-20201012230418206.png)  

<br>

**스택 시간 복잡도**

-   입력하기 : `O(1)`
-   출력하기 : `O(1)`

<br>

**스택 작동 방식**

![image-20201012230437702](README.assets/image-20201012230437702.png)  

<br>

**스택 in Python**

-   배열을 스택(Stack)으로 활용

```python
Stack = []
Stack.append(2)
Stack.append(5)
Stack.pop() #5를 반환
```

<br>

<br>

[실습 4]

## 괄호 매칭

`(`, `)`, `{`, `}`, `<`, `>`, `[`, `]` 의 여덟개의 문자로만 구성된 문자열이 입력으로 주어진다고 해 봅시다.

이때, 이 문자열이 유효한지를 확인하는 함수를 작성 해 보세요.

열린 괄호들이 닫히는 순서가 올바르게 되어 있는 경우에 그 문자열을 유효하다고 합니다.

즉, `({()})` 나 `[]<>{}` 등은 유효한 문자열이며, `)(` `<]` `<(>)` 등은 유효하지 않은 문자열입니다.

<br>

-   “열린 순서대로 닫히는” 것을 어떻게 구현 할 수 있을지 고민 해 보세요.

<br>

```python
def isParenthesisValid(st):
    stack = []
    pDic = {'}' : '{', ']' : '[', ')' : '(', '>' : '<'}
    pOpens = {'{', '[', '(', '<'}
    
    for ch in st:
        if ch in pOpens: # ch가 열린 괄호
            stack.append(ch)
            
        else: # ch가 닫힌 괄호
            if len(stack) != 0 and stack[-1] == pDic[ch]:
                stack.pop()
            
            else:
                return False
    
    if len(stack) != 0:
        return False
        
    return True

def main():
    examples = ["({()})", "[]<>{}", ")(" "<]", "<(>)"]
    for example in examples:
        print(example, isParenthesisValid(example))

    
if __name__ == "__main__":
    main()
```

>   Dictionary key, value를 이용하여 열린 괄호와 닫힌 괄호를 매칭시킴