## 클래스와 메서드

### 클래스와 객체의 정의와 용도

* 클래스의 정의 : 클래스란 객체를 정의해 높은 것이다.

    * 클래스의 용도 : 클래스는 객체를 생성하는데 사용된다.

* 프로그래밍에서 `객체`는 클래스에 정의된 내용대로 **메모리에 생성된 것**을 뜻한다.

* 객체의 정의 : 실제로 존재하는 것. 사물 또는 개념

    * 객체의 용도 : 객체가 가지고 있는 기능과 속성에 따라 다름

### 객체와 인스턴스

* 클래스로부터 객체를 만드는 과정을 클래스의 **인스턴스화(instantiate)** 라고 하며, 어떤 클래스로부터 만들어진 객체를 그 클래스의 **인스턴스(instance)** 라고 한다.

### 객체의 구성요소 - 속성과 기능

* 객체는 속성과 기능, 두 종류의 구성요소로 이루어져 있으며, 일반적으로 객체는 다수의 속성과 다수의 기능을 갖는다.

* 즉, 객체는 속성과 기능의 집합이라고 할 수 있다.

* 속성과 기능은 아래와 같이 같은 뜻의 여러 가지 용어가 있으며, 앞으로 이 중에서도 '속성'보다는 '멤버변수'를, '기능'보다는 '메소드'를 주로 사용할 것이다.

> **속성(property)** : 맴버변수(member variable), 특성(attribute), 필드(filed), 상태(state)

> **기능(function)** : 메소드(method), 함수(function), 행위(behavior)

* 보다 쉽게 이해할 수 있도록 TV를 예로 들어보면 다음과 같다.

    * TV 속성 : 크기, 길이, 높이, 색상, 볼륨, 채널 등

    * TV 기능 : 켜기, 끄기, 볼륨 높이기, 볼륨 낮추기, 채널 변경하기 등

### 인스턴스의 생성과 사용

* 클래스로부터 인스턴스를 생성하는 일반적인 방법은 다음과 같다.

```text
클래스명 변수명;           // 클래스의 객체를 참조하기 위한 참조변수를 선언
변수명 = new 클래스명();   // 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장

Tv t;
t = new Tv();
```

> 인스턴스는 참조변수를 통해서만 다룰 수 있으며, 참조변수의 타입은 인스턴스의 타입과 일치해야한다.

### 객체 배열

* 많은 수의 객체를 다뤄야할 때, 배열로 다루면 편리할 것이다. 객체 역시 배열로 다루는 것이 가능하며, 이를 `객체 배열`이라고 한다.

* 다뤄야할 객체의 수가 많을 때는 for문을 사용하면 된다.

```text
Tv [] tvArr = new  Tv[100];

for(int i = 0; i < tvArr.length; i++) {
    tvArr[i] = new Tv();
}
```

* 모든 배열이 그렇듯이 객체 배열도 **같은 타입의 객체** 만 저장할 수 있다.

* 여러 종류의 객체를 하나의 배열에 저장할 수 있는 방법은 `다형성(polymorphism)`을 통해 가능하다.

### 클래스의 또 다른 정의

* 클래스는 **객체를 생성하기 위한 틀**이며 '클래스는 속성과 기능으로 정의되어 있다.'고 했다. 이것은 객체지향이론의 관점에서 내린 정의이고, 이번에는 **프로그래밍적인 관점**에서 클래스의 정의와 의미를 살펴보도록 하자.

#### 1. 클래스 - 데이터와 함수의 결합

* 프로그래밍언어에서 데이터 처리를 위한 **데이터 저장형태의 발전과정**은 다음과 같다.

> 변수 -> 배열 -> 구조체 -> 클래스

1. 변수 : 하나의 데이터를 저장할 수 있는 공간
2. 배열 : 같은 종류의 여러 데이터를 하나의 집합으로 저장할 수 있는 공간
3. 구조체 : 서로 관련된 여러 데이터를 종류에 관계없이 하나의 집합으로 저장할 수 있는 공간
4. 클래스 : 데이터와 함수의 결합(구조체 + 함수)

* 서로 관련된 변수들을 정의하고 이들에 대한 작업을 수행하는 함수들을 함께 정의한 것이 바로 `클래스`이다.

#### 2. 클래스 - 사용자정의 타입(user - defined type)

* 프로그래밍언어에서 제공하는 자료형(primitive type)외에 프로그래머가 서로 관련된 변수들을 묶어서 하나의 타입으로 새로 추가하는 것을 `사용자정의 타입`이라고 한다.

* 다른 프로그래밍언어에서도 사용자정의 타입을 정의할 수 있는 방법을 제공하고 있으며 자바와 같은 객체지향언어에서는 `클래스`가 곧 `사용자 정의 타입`이다.


## Reference

* [Java의 정석](http://www.yes24.com/Product/Goods/24259565)