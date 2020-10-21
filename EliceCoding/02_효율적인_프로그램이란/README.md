# 시간/공간 복잡도 (Big-O)

**효율성의 측정 방식**

`시간 복잡도` : 알고리즘에 사용되는 총 연산횟수 (코드가 얼마나 빠르게?)

`공간 복잡도` : 알고리즘에 사용되는 메모리 공간의 총량 (얼마나 많은 메모리를 사용?)

<br>

`Big-O 시간 복잡도` = 시간복잡도 함수의 **가장 높은** 차수

aN + b = `O(N)`

aNlogN + b = `O(NlogN)`

aN^2 + bN + c = `O(N^2)`

<br>

배열(list) : `O(N)`

집합(set) : `O(1)`

nums.sort() : `O(NlogN)`

<br>

매번 절반씩 입력값이 줄어들면 `O(logN)`  ex) 이진 탐색

<br>

<br>

[실습 1]

## 중복된 수 제거하기

0보다 큰 정수들이 있는 리스트가 주어집니다. 이 리스트는 작은것부터 큰 순서대로 오름차순 정렬이 되어있으며, 중복을 포함합니다. 이 리스트에서 중복된 수를 없애고 정렬되어있는 리스트를 출력해 봅시다.

예를 들어 `[1, 1, 2, 2, 2, 2, 5, 7, 7, 8]` 이 입력되었다면 중복되어있는 ‘1’ 1개, ‘2’ 3개, ‘7’ 1개를 제거하고 `[1, 2, 5, 7, 8]`을 출력하면 됩니다.

<br>

**O(N)**

```python
def removeDuplicate(nums):
    result = [nums[0]]
    for i in range(1, len(nums)):
        if nums[i] != nums[i-1]:
            result.append(nums[i])
    return result

def main():
    print(removeDuplicate([1, 1, 2, 2, 2, 2, 5, 7, 7, 8])) # [1, 2, 5, 7, 8]을 리턴해야 합니다

if __name__ == "__main__":
    main()
```

<br>

**내 풀이**

```python
def removeDuplicate(nums):
    return list(set(nums))
```

<br>

<br>

[실습 2]

## 0 이동시키기

여러개의 0과 양의 정수들이 섞여 있는 배열이 주어졌다고 합시다. 이 배열에서 0들은 전부 뒤로 빼내고, 나머지 숫자들의 순서는 그대로 유지한 배열을 반환하는 함수를 만들어 봅시다.

예를 들어서, `[0, 8, 0, 37, 4, 5, 0, 50, 0, 34, 0, 0]` 가 입력으로 주어졌을 경우 `[8, 37, 4, 5, 50, 34, 0, 0, 0, 0, 0, 0]` 을 반환하면 됩니다.

이 문제는 공간 복잡도를 고려하면서 풀어 보도록 합시다. 공간 복잡도 O(1)으로 이 문제를 풀 수 있을까요?

<br>

**O(1)** 공간복잡도

```python
def moveZerosToEnd(nums):
	currentPosition = 0
	
	for i in range(len(nums)):
		if nums[i] != 0:
			nums[currentPosition] = nums[i]
			if i != currentPosition:
				nums[i] = 0
			currentPosition += 1
	return nums

def main():
    print(moveZerosToEnd([0, 8, 0, 37, 4, 5, 0, 50, 0, 34, 0, 0]))

if __name__ == "__main__":
    main()
```

<br>

<br>

# 배열

**가장 기본적인 자료 구조**

배열의 공간 복잡도 = `O(N)`

```python
nums = [1, 2, 3, 4, 5, 6]
```

<br>

인덱스를 알 때 : `O(1)`

```python
nums[2]
```

인덱스를 모를 때 = 하나씩 검사 : `O(N)`

```python
if 5 in nums:
```

배열 전부 순회하기 : `O(N)`

```python
for num in nums:
```

자료 끝에 추가하기 : `O(1)`

```python
nums.append(7)
```

자료 중간에 추가하기 : `O(N)`

```python
nums.insert(3, 9)
```

<br>

**문자열**

배열의 한 종류, 문자들의 배열

<br>

**2차원 배열**

행렬

<br>

<br>

[실습 3]

## 배열의 회전

배열을 회전 시켜봅시다. 정수들이 포함되어 있는 배열과, 숫자 k가 입력으로 주어집니다. 이때 해당 배열을 k 만큼 회전 시켜 봅시다.

예를 들어서, `[1, 2, 3, 4, 5, 6, 7, 8, 9]` 와 `4`가 입력으로 주어졌을 경우 `[6,7,8,9,1,2,3,4,5]` 를 반환하면 됩니다.

-   k 는 배열의 길이 n 보다 작다고 가정합시다.
-   다양한 방법으로 풀어 보도록 합시다.
-   (추가) 공간 복잡도 O(1)으로 풀 수 있는 방법도 생각 해 봅시다. 이때 주어진 함수 partialReverse를 활용해도 됩니다.

<br>

```python
# 이 함수를 수정 해 주세요.
def rotateArray(nums, k):
    return nums[len(nums)-k:] + nums[:len(nums)-k]

def main():
    nums = [1,2,3,4,5]
    print(rotateArray([1,2,3,4,5,6,7,8,9], 4)) # [6,7,8,9,1,2,3,4,5] 를 반환해야 합니다.
    
if __name__ == "__main__":
    main()
```

<br>

partialReverse 활용

```python
# 다음 함수는 추가적인 공간 사용 없이 배열의 일부를 뒤집어 주는 함수입니다.
# 예를 들어, nums = [1,2,3,4,5]
# partialReverse(nums, 1, 3)
# 을 실행 할 경우, nums = [1, 4, 3, 2, 5] 가 됩니다.
# 필요하다면 사용하세요.
def partialReverse(nums, start, end):
    for i in range(0, int((end-start)/2) + 1):
        temp = nums[start + i]
        nums[start+i] = nums[end - i]
        nums[end -i] = temp
        
def rotateArray(nums, k):
    partialReverse(nums, 0, len(nums)-1)
    partialReverse(nums, 0, k-1)
    partialReverse(nums, k, len(nums)-1)
    
    return nums
```

<br>

<br>

# 해쉬

**Dictionary.Key + Value (in Python)** : key에 value를 저장하는 자료구조

Key는 중복될 수 없음

공간 복잡도는 대략 `O(N)`

```python
studentIds = {
“박지나”:123,
“송호준”:145,
“이주원”:563 }
```

<br>

Key를 이용해서 Value 가져오기 : 대략 `O(1)`

```python
print(studentIds[“박지나”])
```

Key가 존재하는지 확인하기 : 대략 `O(1)`

```python
if(“박지나” in studentIds):
if(“손지윤” in studnetIds):
```

Key, Value 추가하기 : 대략 `O(1)`

```python
studentIds[“손지윤”] = 938
```

해당 Key의 Value 변경하기 : 대략 `O(1)`

```python
studentIds[“박지나”] = 555
```

<br>

해쉬의 공간 복잡도 = `O(N)`

해쉬는 데이터가 입력되지 않은 여유 공간이 많아야 성능 유지

<br>

**Set**

Value 없이 **Key**만 있는 Dictionary

```python
studentNames = {“박지나”, “송호준”, “이주원”, “손지윤”}
```

<br>

<br>

[실습 4]

## 아나그램 탐지

아나그램(Anagram)은 한 문자열의 문자를 재배열해서 다른 뜻을 가지는 다른 단어로 바꾸는 것을 의미합니다.

두 개의 문자열이 주어졌을 때, 서로가 서로의 아나그램인지 아닌지의 여부를 탐지하는 함수를 만들어 보세요.

-   `elice` 와 `leice` 는 아나그램입니다. `True`를 리턴해야 합니다.
-   `cat` 과 `cap` 는 아나그램이 아닙니다. `False` 를 리턴해야 합니다.
-   `iamlordvoldemort` 와 `tommarvoloriddle` 은 아나그램입니다. `True`를 리턴해야 합니다.
-   문자열의 모든 문자는 영어 소문자라고 가정합시다.

<br>

List 활용

```python
def isAnagram(str1, str2):
    str1List = list(str1)
    str2List = list(str2)
    str1List.sort()
    str2List.sort()
    return (str1List == str2List)

def main():
    print(isAnagram('iamlordvoldemort', 'tommarvoloriddle')) # should return True
    print(isAnagram('cat', 'cap')) #should return False

if __name__ == "__main__":
    main()
```

<br>

Dictionary 활용

```python
def isAnagram(str1, str2):
    dic1 = {}
    for ch in str1:
        dic1[ch] = dic1.get(ch, 0) + 1
        
    for ch in str2:
        if ch in dic1:
            if dic1[ch] == 0:
                return False
            else:
                dic1[ch] -= 1
        else:
            return False
    return True
```

<br>

<br>

# 배열과 해쉬의 trade-off

**배열 VS 해쉬**

`해쉬` : 식별자가 있는 데이터, 시간 복잡도↓ `O(1)`/ 공간 복잡도↑ (충돌 방지)

`배열` : 식별자가 없는 데이터, 시간 복잡도↑/ 공간 복잡도↓ `O(N)`