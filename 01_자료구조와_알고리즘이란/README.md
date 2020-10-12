`자료구조` : 데이터를 저장할 때 필요한 구조 (Data Structure)

`알고리즘` : 프로그램을 어떻게 실행 → 계산절차

`객체` : 상태(state, property) + 행동(behavior, method)



## 자동차 객체

Python은 세상의 모든 것을 객체(object)로 바라봅니다.

이 문제에는 자동차 객체가 주어져 있는데요, 아직 불완전한 상태입니다.

객체에 변수와 함수들을 추가해서 완성 해 봅시다.





## 풀어보세요

1.  변수 color를 추가 해 봅시다.
2.  함수 speedDown을 추가 해 봅시다.
3.  함수 changeColor를 추가 해 봅시다.
4.  함수 wheelChange의 내용을 변경 해 봅시다.



기존

```python
class Car:
    def __init__(self):
        self.speed = 0
        self.year = 2017
        self.wheel = Wheel("aluminum")
        # 1. 여기에 새로운 오브젝트 변수, color를 추가 해 주세요.
        # 색은 기본적으로 "white"로 설정되도록 해 주세요
        
    def speedUp(self, addSpeed):
        self.speed += addSpeed
        
    # 2. 여기에 새로운 오브젝트 함수, speedDown을 추가해 주세요
    # 변화시키고 싶은 속도량을 입력 받은 후, 그만큼 속도록 감소시키는 일을 하는 함수입니다.
    
    # 3. 여기에 새로운 함수, changeColor를 추가 해 봅시다.
    # 변화시키고 싶은 색을 지정하면, 그 색깔로 차를 도색하는 함수입니다.    


    def wheelChange(self, newWheelType):
        pass
        # 4. 객체의 데이터로 다른 객체를 사용 할 수도 있습니다. 
        # Car 객체는 Wheel 객체를 변수로 가지는데요, 
        # 여기에는 새 바퀴의 색상을 입력받고(newWheelType), 이를 바탕으로 새로운 Wheel 객체를 만들어서
        # 자동차의 wheel 데이터에 할당 하는 함수를 적어 봅시다.
    

class Wheel:
    def __init__(self, newWheelType):
        self.wheelType = newWheelType

def main():
    audi = Car()
    print("고객님의 차량은 {} 년에 출고되었습니다.".format(audi.year))
    print("현재 속도는 {} km/h 입니다.".format(audi.speed))
    audi.speedUp(200)
    print("변경된 속도는 {} km/h 입니다.".format(audi.speed))
    
    randomWheel = Wheel("aluminum")
    print("바닥에 {} 재질의 바퀴가 떨어져 있습니다.".format(randomWheel.wheelType))
    
if __name__ == "__main__":
    main()
```

  

결과

```python
class Car:
    def __init__(self):
        self.speed = 0
        self.year = 2017
        self.wheel = Wheel("aluminum")
        self.color = "white"
        # 1. 여기에 새로운 오브젝트 변수, color를 추가 해 주세요.
        # 색은 기본적으로 "white"로 설정되도록 해 주세요
        
    def speedUp(self, addSpeed):
        self.speed += addSpeed
        
    def speedDown(self, subSpeed):
        self.speed -= subSpeed
        
    # 2. 여기에 새로운 오브젝트 함수, speedDown을 추가해 주세요
    # 변화시키고 싶은 속도량을 입력 받은 후, 그만큼 속도록 감소시키는 일을 하는 함수입니다.
    def changeColor(self, newColor):
        self.color = newColor
    # 3. 여기에 새로운 함수, changeColor를 추가 해 봅시다.
    # 변화시키고 싶은 색을 지정하면, 그 색깔로 차를 도색하는 함수입니다.    


    def wheelChange(self, newWheelType):
        self.wheel = Wheel(newWheelType)
        # 4. 객체의 데이터로 다른 객체를 사용 할 수도 있습니다. 
        # Car 객체는 Wheel 객체를 변수로 가지는데요, 
        # 여기에는 새 바퀴의 색상을 입력받고(newWheelType), 이를 바탕으로 새로운 Wheel 객체를 만들어서
        # 자동차의 wheel 데이터에 할당 하는 함수를 적어 봅시다.
    

class Wheel:
    def __init__(self, newWheelType):
        self.wheelType = newWheelType

def main():
    audi = Car()
    print("고객님의 차량은 {} 년에 출고되었습니다.".format(audi.year))
    print("현재 속도는 {} km/h 입니다.".format(audi.speed))
    audi.speedUp(200)
    print("변경된 속도는 {} km/h 입니다.".format(audi.speed))
    
    randomWheel = Wheel("aluminum")
    print("바닥에 {} 재질의 바퀴가 떨어져 있습니다.".format(randomWheel.wheelType))
    
if __name__ == "__main__":
    main()
```

