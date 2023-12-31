# 불변 활용하기 

## 1. 재할당 
변수에 값을 다시 할당하는 것을 `재할당` or `파괴적 할당`이라고 한다. `java`에서는 `final`을 통해서 변수의 재할당을 막을 수 있다.    
</br></br></br>
     
## 2. 가변으로 인해 발생하는 의도하지 않은 영향
#### 1) 가변 인스턴스 재사용하는 경우 
  특정 변수나 객체를 재사용하여 여러 곳에서 사용하는 경우, 예상하지 못하게 바뀔 수 있다.    
#### 2) 함수로 가변 인스턴스 조작하기 
  함수 내에서 변수들의 상태를 변화시키는 경우, 여러 스레드 간의 실행 순서에 의해 의도하지 않는 값이 나올 수 있다.    
</br>

### 부수효과의 단점 
'주요 작용 이외의 상태 변경을 일으키는 것'

#### 상태 변경되는 상황 
- 인스턴스 변경
- 전역 변수 변경
- 매개변수 변경
- 파일 읽고 쓰는 I/O 조작

> 파일 I/O도 상태 변경에 포함된다. 파일을 읽을 때 or 쓸때 변경되는지 시점을 알수 없다.

> 함수 내부에서 변수들의 값을 변경시키는 것이 정말 위험하다. 
</br>

### 함수의 영향 범위 한정하기 
- 데이터(상태)는 매개변수로 받기
- 상태는 변경하지 않기
- 값은 함수의 리턴 값으로 돌려주기
> 부수 효과로 인한 범위를 클래스 내부로 최소한 좁히기  
</br>

### 불변으로 만들어서 예기치 못한 동작 막기 
기능 변경 때에 의도하지 않게 부수 효과가 있는 함수가 만들어져서, 예상하지 못한 동작을 일으킬 가능성은 항상 존대한다. 프로젝트가 클수록 더 커짐. 
</br></br>

## 3. 불변과 가변은 어떻게 다루어야 할까? 
`예측 가능하기 쉬움`, `변수 의미 유지`, `코드 영향 범위를 한정할 수 있어 유지보수가 편함`의 측면에서 불변으로 변수를 선언하는 것이 좋다. 
</br>

### 가변으로 설계해야 하는 경우
1. 성능 측면
  대량의 데이터를 빠르게 처리 하는 경우, 이미지 처리하는 경우, 리소스에 제약이 큰 임베디드 소프트웨어를 다루는 경우 등은 가변을 사용하는 것이 좋다.

2. 변수 사용 스코프가 국소적인 경우
   특정 파일 내부에서만 사용하는 지역 변수의 경우 가변으로 해도 괜찮다.
</br>

#### 코드 외부와 데이터 교환은 국소화하기 
- `Repository Pattern`: 데이터 레이어와 비즈니스 로직을 분리하는 패턴. 데이터 레이어를 추상화 시키고, 데이터를 사용하는 곳에서는 객체를 가져가서 사용할 수 있도록 하는 것.
</br></br></br>

## 번외
**1. Abstraction 이란?**    

fundamental concept. 구체적인/불필요한 로직을 제외하고, 대략적인 틀, 로직만 보여주는 것.    

추상화가 필요한 이유는, 
1. 내부의 세부적인 로직을 숨길 수 있다.
2. 사용자가 대략적인 것만 알면 쓸수 있다. 구지 모든 것을 알 필요가 없다. 

**2. Repository Pattern on Android**   

api를 통해 데이터를 가져와서 필요한 데이터(객체)로 변환 후의 memory or db에 저장해놓는 패턴이다. 이 책을 읽으면서, 데이터 변경 가능성을 최소한으로 하기 위해서 `repository pattern`을 사용한다는 것을 배웠다. (기존에는 관심사 분리하기 위하 정도로만 이해했다) 



