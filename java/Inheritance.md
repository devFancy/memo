## 상속

상속이란, 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다.

자식이 부모로부터 상속받고자 할 경우, 자식 클래스 뒤에 ‘extends’를 함께 써주면 된다.

상속받는 것은 조상 클래스를 확장(extend)한다는 의미로 아래 2가지 조건을 만족한다.

- 생성자와 초기화 블록은 상속되지 않는다.
- 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.

예를 들어,

`조상 클래스 - 자손 클래스 - 자손의 자손 클래스`가 있다고 가정해본다.

이때, 조상 클래스만 변경해도 모든 자손 클래스에, 자손의 자손 클래스에까지 영향을 미치기 때문에,

클래스간의 **상속 관계**를 맺어주면

**자손 클래스들의 공통적인 부분**은 `조상 클래스`에서 관리하고

`자손 클래스`는 **자신에 정의된 멤버들만 관리**하면 되므로

각 클래스의 코드가 적어져서 관리가 쉬워진다.


## super 및 super( )의 용도

1) `super`는 자신이 상속받은 부모 클래스에 대한 참조 변수로,부모 클래스의 멤버에 접근할 때 사용된다.

   - 주로 객체안에 있는 **부모의 멤버변수와 자신의 멤버변수를 구별**하기 위해 사용된다.

2) `super()`는 자식 클래스의 생성자에서 부모 클래스의 생성자를 호출하기 위해서 사용된다.

   - `super()`는 생성자 코드안에서 사용 될 때, 다른 코드에 앞서 **첫줄에 사용**되어야 한다.
   - 자식 클래스의 모든 생성자는 **부모 클래스의 생성자를 포함**하고 있어야 한다. 그런데 **만약 자식 클래스의 생성자에 부모 클래스의 생성자가 지정되어 있지 않다면, `컴파일러`가 자동으로 부모 클래스의 기본 생성자를 호출한다.**
   - (이러한 경우, 부모클래스에 매개변수가 있는 생성자만 있고, 기본 생성자가 없어 기본 생성자를 호출할수 없다면 에러가 발생합니다.)

### 사용예제

> Book 클래스 정의 (부모클래스)

```java
public class Book {

	String title ="미입력";
	int price = -1;
	int code = 100;
		
	public Book() {  	}                     // 기본생성자
		
	public Book(String title, int price) {      // 매개변수 2개인 생성자
		this.title = title;
		this.price = price;
	}

	
	public void showPrice() {
		System.out.println(title + "의 가격은 " + price + "원 입니다");
	}
}
```

> EnglishBook 클래스 정의 (자식클래스)

```java
public class EnglishBook extends Book {

	int code = 200;
	
	public EnglishBook() {    }                       // 기본생성자

	public EnglishBook(String title, int price) {    // 매개변수 2개인 생성자
		super(title, price);     
	}

	
	public void showPrice() {

		super.showPrice();      // 부모클래스의 메소드 호출
		
		System.out.println("");
		System.out.println("code       : " + code);
		System.out.println("this.code  : " + this.code);
		System.out.println("super.code : " + super.code);
		
		System.out.println("");
		System.out.println("price       : " + price);
		System.out.println("this.price  : " + this.price);
		System.out.println("super.price : " + super.price);
	
	}
}
```

> 객체 생성 및 실행

```java
public class HelloWorld {
	public static void main(String[] args) {

		EnglishBook b1 = new EnglishBook("영어책", 1000);
		b1.showPrice();
	}
}
```

> 실행결과

![](/img/java-super-result.png)

## Reference

- [Java의 정석](http://www.yes24.com/Product/Goods/24259565)
- https://kadosholy.tistory.com/93