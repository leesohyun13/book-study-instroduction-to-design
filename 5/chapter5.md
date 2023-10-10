# 응집도: 흩어져 있는 것들    

> 응집도는 클래스 내부에서 데이터와 로직의 관계가 얼마나 강한지 나타내는 지표
</br>

## 1. static 메서드 요용   
### 인스턴스 변수를 사용하는 구조로 변경하기 
- static 메서드를 만드는 순간, 데이터와 그 로직사이의 괴리가 생김.   

> 그래서 kotlin에서는 `companion object`를 사용해서 응집도를 높이면서 메모리 관리까지 하려는간가..?

- staic 메서드를 사용하는 이유는 C언어와 같은 절차 지향언어의  접근 방법을 사용하려고 하는 것임. 절차 지향 언어에서는 데이터와 로직을 따로 존재하도록 설계함.
- static은 응집도의 영향을 받지 않는 '로그 출력 전용 메소드', '포멧 변환 전용 메서드'처럼 응집도와 관계없는 기능을 static으로 만들어서 설계하는 것이 좋음. 예로, 팩토리 메서드.
</br>

## 2. 초기화 로직 분산
- 클래스를 잘 설계해도, 초기화 로직이 분산되어 응집도가 낮은 구조가 될 수 있음.
- `private` + 팩토리 메서드를 사용해, 목적에 따라 초기화하기.
- 생성로직이 많아지면 팩토리 클래스를 고려해보자.
</br>

## 3. 범용 전용 클래스
- 범용 전용 클래스가 위험한 이유는 **너무 많은 로직인 한 클래스에 모이는 문제**입니다. `범용`과 `재사용성`의 의미를 혼동하는 경우입니다. 재사용성은 설계의 응집도를 높이면, 저절로 높아진다. 
- 횡단 관심사만 범용으로 가능; 그외에는 재사용성을 고려한 객체 설계 방향으로 해야한다. 
    - 로그 출력
    - 오류 확인
    - 디버깅
    - 예외처리
    - 캐시
    - 동기화
    - 분산처리
</br>

## 4. 결과를 리천하는 데 매개변수 사용하지 않기 


## 번외
### 언제, 왜 kotlin에서 extension을 사용할까? 
- `inline function`
```
inline fun <reified T, reified U> ObjectMapper.addMixIn(): ObjectMapper = this.addMixIn(T::class.java, U::class.java)
``` 
- Operator overloading﻿ like `*`, `+`
```
class OrdersList: IndexedContainer {
    override fun get(index: Int) { /*...*/ }
}
```
- iterator() extension method
- 특정 스코프 or Context에서 계산 로직을 만들고 싶은 경우 
</br>
