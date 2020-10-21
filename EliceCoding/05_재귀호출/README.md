[실습1]

## k번째 수 찾기

n개의 숫자가 차례대로 주어질 때, 매 순간마다 “지금까지 입력된 숫자들 중에서 k번째로 작은 수”를 반환하는 프로그램을 작성하세요.

프로그램의 입력으로는 첫째줄에 n과 k가 입력되고, 둘째줄에 n개의 숫자가 차례대로 주어집니다.

#### 입력 예시

```
10 3
1 9 8 5 2 3 5 6 2 10
```

#### 출력 예시

```
-1 -1 9 8 5 3 3 3 2 2
```

<br>

#### 문제 조건

-   n은 100보다 작은 숫자입니다.
-   매 순간마다 지금까지의 입력중 k번째로 작은 수를 출력하되, 없다면 -1을 출력합니다.

#### 입출력 예시 설명

10개의 숫자가 차례대로 주어집니다. 맨 처음 1만 입력을 받았을 경우, 3번째로 작은 숫자가 없으므로 -1을 출력합니다. 그 다음 9도 마찬가지입니다. 세 번째로 숫자 8을 입력받는 순간, 지금까지 입력받은 숫자는 1, 9, 8 세 개이고, 이 중 3 번째로 작은 숫자인 9를 출력합니다. 마찬가지로 숫자 하나를 입력받을 때 마다 3번째로 작은 숫자를 출력합니다.

<br>

```python
def findKth(myInput, k) :
    '''
    매 순간마다 k번째로 작은 원소를 리스트로 반환합니다.
    '''

    result = []
    data = []
    
    for element in myInput:
        data.append(element)
        data.sort()
        
        '''
        data[k-1] = 우리가 찾는 값
        data에 들어 있는 수가 k보다 작을 때?
        '''
        
        if len(data) < k:
            result.append(-1)
        else:
            result.append(data[k-1])

    return result

def main():
    firstLine = [int(x) for x in input().split()]
    myInput = [int(x) for x in input().split()]

    print(*findKth(myInput, firstLine[1]))
    
if __name__ == "__main__":
    main()
```

<br>

<br>

<br>

[실습 2]

## quick sort

입력으로 n개의 수가 주어지면, quick sort를 구현하는 프로그램을 작성하세요.

#### 입력 예시

```
10 2 3 4 5 6 9 7 8 1
```

#### 출력 예시

```
1 2 3 4 5 6 7 8 9 10
```

<br>

```python
def quickSort(array):
    '''
    퀵정렬을 통해 오름차순으로 정렬된 array를반환하는 함수를 작성하세요.
    '''
    if len(array) <= 1:
        return array
        
    pivot = array[0]
    
    left = getSmall(array[1:], pivot)
    right = getLarge(array[1:], pivot)
    
    return quickSort(left) + [pivot] + quickSort(right)
        

def getSmall(array, pivot):
    data = []
    for a in array:
        if a <= pivot:
            data.append(a)
    return data
            
def getLarge(array, pivot):
    data = []
    for a in array:
        if a > pivot:
            data.append(a)
    return data

def main():
    line = [int(x) for x in input().split()]

    print(*quickSort(line))

if __name__ == "__main__":
    main()
```

<br>

<br>

<br>

[실습 3]

## 올바른 괄호인지 판단하기

본 문제에서는 입력으로 주어지는 괄호가 올바른 괄호인지를 판단하는 프로그램을 작성합니다.

예를 들어, ‘(())’ 은 올바른 괄호이지만, ‘(()))’, 혹은 ‘(()()(‘ 는 올바른 괄호가 아닙니다.

올바른 괄호일때 ‘YES’를, 올바르지 않은 괄호일때 ‘NO’를 출력해 봅시다.

#### 입력 예시 1

```
(())()
```

#### 출력 예시 1

```
YES
```

#### 입력 예시 2

```
(((())())(()())((())()))
```

#### 출력 예시 2

```
YES
```

#### 입력 예시 3

```
(())())()
```

#### 출력 예시 3

```
NO
```

#### 입력 예시 4

```
((()())(()())))(())
```

#### 출력 예시 4

```
NO
```

<br>

#### 입력

괄호 p가 주어집니다.

#### 출력

p가 올바른 괄호이면 YES, 그렇지 않으면 NO를 출력합니다.

<br>

```python
def checkParen(p):
    '''
    괄호 문자열 p의 쌍이 맞으면 "YES", 아니면  "NO"를 반환
    
    1. 기저조건 처리
    2. p에서 인접한 괄호쌍을 찾아 제거
    3. checkParen() 함수에 다시 물어본다.
    '''
    
    if len(p) == 0 :
        return "YES"
    elif len(p) == 1:
        return "NO"
        
    for i in range(len(p)-1):
        if p[i] == '(' and p[i+1] == ')':
            q = p[:i] + p[i+2:]
            return checkParen(q)
            
    return "NO"

def main():

    x = input()
    print(checkParen(x))

if __name__ == "__main__":
    main()
```

<br>

<br>

<br>

[보조 1]

## 이진수 변환

10진수를 2진수로 변환하여 출력하는 프로그램을 작성하세요. **단, 재귀호출을 이용하여 작성합니다.**

#### 입력 예시

```
19
```

#### 출력 예시

```
10011
```

<br>

#### 문제 조건

-   입력되는 10진수는 1,000,000 이하의 자연수 입니다.

<br>

```python
import sys
sys.setrecursionlimit(100000)

def convertBinary(n) :
    '''
    10진수 n을 2진수로 변환하여 반환합니다.

    *주의* : 변환된 2진수는 문자열이어야 합니다.

    예를 들어, 19가 입력될 경우 문자열 "10011"이 반환되어야 합니다.
    '''
    if n==0 or n==1:
        return str(n)
        
    if n%2 == 1:
        return str(convertBinary(n//2)) + "1"
    else:
        return str(convertBinary(n//2)) + "0"

def main():

    n = int(input())

    print(convertBinary(n))

if __name__ == "__main__":
    main()
```

