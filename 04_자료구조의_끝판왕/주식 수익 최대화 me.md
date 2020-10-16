## 주식 수익 최대화

주식 가격을 나타내는 숫자들의 배열이 주어집니다. 즉, 배열의 인덱스 i의 숫자가 해당 시간의 주식 가격입니다.

주식 한 주를 단 한번 사고 단 한번 팔 수 있다고 합시다. 이때 최대 수익을 구해내는 알고리즘을 구현 해 보세요.

예를 들어서,

`1, 2, 3, 4, 5, 6, 7` 과 같은 경우엔 1일때 사서 7일때 파는게 가장 이득입니다. 따라서 6을 반환하면 됩니다.

`7, 6, 5, 4, 3, 2, 1` 과 같은 경우에는 주식 가격이 쭉 하락했으므로, 이득을 낼 수 없습니다. 0을 반환하면 됩니다.

`1, 2, 3, 4, 3, 2, 1` 과 같은경우엔 1일때 사서 4일때 파는게 가장 이득입니다. 3을 반환하면 됩니다.

`2, 8, 19, 37, 4, 5` 와 같은경우엔 2일때 사서 37일때 파는게 가장 이득입니다. 35를 반환하면 됩니다.

<br>

내 풀이 O(n) (이중 for문으로 O(n^2) 도 가능)

```python
# O(n)
def maximizeProfit(nums):
    n = len(nums)
    max_profit = 0 # 이득이 없을 때 0을 반환
    price = nums[0]  # 1일 우선 저장, 감소할 때까지
    for num in nums: # nums 순회
        profit = num - price # 수익 계산
        if profit > max_profit: # 수익이 더 큰 경우를 찾으면 넣어줌
            max_profit = profit
        if num < price: # 1일 우선 저장, 감소할 때까지
            price = num
    return max_profit

def main():
    print(maximizeProfit([1,2,3,4,5,6,7])) # 6
    print(maximizeProfit([7,6,5,4,3,2,1])) # 0
    print(maximizeProfit([1,2,3,4,3,2,1])) # 3
    print(maximizeProfit([2,8,19,37,4,5])) # 35

if __name__ == "__main__":
    main()
```

