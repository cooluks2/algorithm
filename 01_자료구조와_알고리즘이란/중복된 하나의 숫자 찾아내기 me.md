## 중복된 하나의 숫자 찾아내기

숫자들의 배열이 주어집니다. 이 배열은 길이 n을 가지며, 1부터 n-1까지의 숫자로 이루어져있습니다.
모든 숫자가 배열에 단 한번씩만 나타납니다. 그런데, 딱 하나의 수가 배열에 두번 등장합니다.
이 중복되는 숫자를 찾아내어 보세요.

예를 들어서, `[1, 5, 2, 4, 5, 6, 3]` 를 살펴봅시다. 배열의 길이는 7이며, 따라서 1~6까지의 숫자들이 한번씩 등장합니다. 그런데 5만 한번 더 등장했네요.따라서 이 경우에는`5`를 찾아내면 됩니다.



```python

def findDuplicate(nums):
    for n in range(1, len(nums)):
        nums.remove(n)
        
    return nums[0]


def main():
    print(findDuplicate([1, 5, 2, 4, 5, 6, 3]))

if __name__ == "__main__":
    main()
```

>   효율성 테스트 미통과



```python
def findDuplicate(nums):
    nums.sort()
    for n, num in enumerate(nums,1):
        if n != num:
            return num

def main():
    print(findDuplicate([1, 5, 2, 4, 5, 6, 3]))

if __name__ == "__main__":
    main()
```

>   통과