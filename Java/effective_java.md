# Effective Java

# 목차
- 1-1 [생성자 대신 static 팩토리 메소드 사용을 고려하자](#생성자-대신-static-팩토리-메소드-사용을-고려하자)
- 1-2 [생성자의 매개변수가 많을 때는 빌더를 고려하자](#생성자의-매개변수가-많을-때는-빌더를-고려하자)
- 1-3 [private 생성자나 enum 타입을 사용해서 싱글톤의 특성을 유지하자](#private-생성자나-enum-타입을-사용해서-싱글톤의-특성을-유지하자)
- 1-4 [private 생성자를 사용해서 인스턴스 생성을 못하게 하자](#private-생성자를-사용해서-인스턴스-생성을-못하게-하자)
# 생성자 대신 static 팩토리 메소드 사용을 고려하자

## 생성자
객체 기반의 프로그래밍을 하다보면 객체를 생성하여야 한다. 객체를 생성한다를 다른 표현으로 인스턴스를 생성한다라고 하며 해당 클래스의 객체를 생성하기 위해서는 public 생성자가 제공되어야 한다.
아래는 일반적인 객체 생성의 예이다.
```java
Car car = new Car();
```
위와 같이 객체를 생성하기 위해서는 Car 클래스에 public 생성자가 필요하다는 것이다.
책에서는 생성자 대신 static 팩토리 메소드 사용을 고려하자는데 이게 무슨 말인지 알아보자.
## static 팩토리 메소드
```java
public static Boolean valueOf(boolean b){ 
    return b ? Boolean.TRUE : Boolean.FALSE; 
   # }
```
위에 코드는 책에 나오는 예제이다.
클래스에서는 생성자를 대신하거나, 또는 생성자에 부가하여 static 팩토리 메소드를 가질 수 있다.
static 팩토리 메소드를 제공하면 다음과 같은 장단점이 있다.
## 장점
1. 생성자와 달리 자기 나름의 이름을 가질 수 있다.
- 생성자는 클래스 이름과 동일해야 한다. static 팩토리 메소드를 사용하면 얼마든지 매개변수와 반환 객체를 잘 표현할 수 있는 메소드 네이밍이 가능하다.

2. 생성자와 달리 호출될 때마다 매번 새로운 객체를 생성할 필요가 없다.
- 불변 클래스의 경우 이미 생성된 인스턴스를 다시 사용할 수 있으며, 불필요하게 중복된 인스턴스들이 생성되는 것을 방지하기 위해 이미 생성된 인스턴스들을 저장했다가 반복 사용할 수 있다.
- static 팩토리 메소드는 여러번 호출되더라도 이미 생성된 동일 객체를 반환할 수 있으며 이 기법은 Flyweight 패턴과 유사하다.

3. 자신의 클래스 인스턴스만 반환하는 생성자와 달리 static 팩토리 메소드는 자신이 반환하는 타입의 어떤 서브타입 객체도 반환할 수 있다.
- 반환되는 객체의 클래스를 선택 해야 할 때 뛰어난 유연성을 제공한다.

## 단점

1. 인스턴스 생성을 위해 static 팩토리 메소드만 갖고 있으면서 public이나 protected 생성자가 없는 클래스의 경우는 서브 클래스를 가질 수 없다.
- 하지만 이런 단점이 장점이 될 수도 있다. 프로그래머들이 상속 대신 컴포지션을 사용하게끔 해 주기 때문이다.

2. 다른 static 메소드와 쉽게 구별 할 수 없다.
- API 문서에서 static 팩토리 메소드를 쉽게 알 수 있도록 javadoc에서 언젠가 해주겠지만 그전에는 주석으롶 표시를 하거나 공통적인 작명 규칙을 만들고 지킴으로써 이러한 단점을 줄일 수 있다.
 - valueOf - 자신의 매개변수와 같은 값을 갖는 인스턴스를 반환한다. 이런 static 팩토리는 타입을 변환하는 메소드 이다.
 - of - valueOf를 줄인 형태의 이름이며, EnumSet에서 사용한다.
 - getInstance - 매개변수에 나타난 인스턴스를 반환하지만, 매개변수와 같은 값을 갖지 않을 수도 있다. singleton의 경우 매개변수는 없으며 오직 하나의 인스턴스만 반환
 - newInstance - getInstance와 유사하나 반환되는 각 인스턴스가 서로 다르다.
 - getType - getInstance와 유사하나 팩토리 메소드가 다른 클래스에 있을 때 사용한다. 여기서 Type은 팩토리 메소드에서 반환되는 객체의 타입을 나타낸다.
 - newType - newInstance와 유사하나 팩토리 메소드가 다른 클래스에 있을 때 사용한다. 여기소 Type은 팩토리 메소드에서 반환되는 객체의 타입을 나타낸다.

## 요약
static 팩토리 메소드와 public 생성자는 모두 나름의 용도가 있으므로 상호간의 장점을 아는 것이 중요하다. 대게 static 팩토리 메소드가 더 좋을때가 많으므로 고려하지 않고 public 생성자를 사용하는 습관을 피하자 

# 생성자의 매개변수가 많을 때는 빌더를 고려하자
매개변수가 많아질 경우 해당 클래스의 객체를 생성하려면 신축성 있게 처리하지 못한다.

## 해결방안

1. 텔리스코핑 생성자 패턴
필수 매개변수들만 갖는 생성자, 필수 매개변수들과 선택 매개변수 하나를 갖는 생성자, 필수 매개변수들과 선택 매개변수 두 개를 갖는 생성자 등의 형태로 모든 선택 매개변수를 생성자가 가질 수 있도록 여러 개의 생성자를 겹겹이 만드는 방법이다.
적은 매개변수만 사용한다면 그리 나쁜 것 같지 않지만 매개변수의 수가 증가하면 무척 번거로워진다.

2. 자바빈즈 패턴
매개변수가 없는 생성자를 호출해서 객체를 생선한 후 세터(setter) 메소드를 호출해서 각각의 필수 필드와 선택 필드 값을 지정한다.
```java
// 자바빈즈 패턴
public class CafeMenu {
	private int coffee = 1;		//필수 
	private int beverage = 1;	//필수 
	private int dessert = 0;	//선택 
	private int bakery = 0;		//선택
	private int drinks = 0;		//선택 
	public CafeMenu(){}
	//setter 
	public void setCoffee(int coffee) {
		this.coffee = coffee;
	}
	public void setBeverage(int beverage) {
		this.beverage = beverage;
	}
	public void setDessert(int dessert) {
		this.dessert = dessert;
	}
	public void setBakery(int bakery) {
		this.bakery = bakery;
	}
	public void setDrinks(int drinks) {
		this.drinks = drinks;
	}
```
코드가 조금 길어지기는 하지만 인스턴스 생성이 간단하고 코드의 가독성도 좋다.
하지만 1회의 호출로 객체생성을 끝낼 수 없으므로 객체의 일관성이 깨질 수 있다. 또한 큰 단점으로 자바빈즈 패턴은 불변 클래스를 만들 수 있는 가능성을 배제하므로 스레드에서 안전성을 유지하려면 프로그래머의 추가적인 노력이 필요하다는 단점이 있다.
3. 빌더 패턴
빌더 패턴은 텔리스코핑 생성자 패턴의 안전성과 자바빈즈 패턴의 가독성을 결합한 방법이다.
원하는 객체를 바로 생성하는 대신 클라이언트는 모든 필수 매개변수를 갖는 생성자를 호출하여 빌더 객체를 얻는다. 그 다음에 빌더 객체의 세터 메소드를 호출하여 필요한 선택 매개변수들의 값을 설정한다. 마지막으로, 클라이언트는 매개변수가 없는 build 메소드를 호출하여 불변 객체를 생성한다.
```java
// 빌더 패턴
public class NutritionFacts{
    private final int servingSize; // 필수 매개변수
    private final int servings; // 필수 매개변수
    private final int calories; // 선택 매개변수
    private final int fat; // 선택 매개변수

    public static class Builder{
        private final int servingSize;
        private final int servings;

        private int calories = 0; // 선택 매개변수 초기화
        private int fat = 0; // 선택 매개변수 초기화
        public Builder(int servingSize, int servings){
            this.servingSize = servingSize;
            this.servings = servings;
        }
        public Builder calories(int val){
            calories = val; return this;
        }
        public Builder fat(int val){
            fat = val; return this;
        }
        public NutritionFacts build(){
            return new NutritionFacts(this);
        }
    }
    private NutritionFacts(Builder builder){
        servingSize = builder.servingSize;
        servings = builder.servings;
        calories = builder. calories;
        fat = builder.fat;
    }
// 사용
NutritionFacts cocaCola = new NutritionFacts.builder(1,1).calories(10).bulid();
```
## 요약
생성자나 static 팩토리 메소드에서 많은 매개변수를 갖게 되는 클래스를 설계할 때는 필더 패턴이 좋은 선택이다.

# private 생성자나 enum 타입을 사용해서 싱글톤의 특성을 유지하자

## 싱글톤
디자인 패턴 중 가장 간단하면서도 자주 사용하는 패턴 중 하나이며 하나의 인스턴스만 생성되는 클래스이다.

1. public final 필드를 갖는 싱글톤
```java
public class Elvis{
    public static final Elvis INSTANCE = new Elvis();
    private Elvis(){...}
    public void leaveTheBuilding(){

    }
}
```
2. static 팩토리 메소드를 갖는 싱글톤
```java
public class Elvis{
    private static final Elvis INSTANCE = new Elvis();
    private Elvis(){...}
    public static Elvis getInstance(){return INSTANCE;}
    public void leaveTheBuilding(){
    }
}
```
이 방법의 이점은 클래스에서 반환하는 싱글톤 인스턴스의 형태를 변경할 수 있는 유연성을 제공한다.

위 두 가지 방법으로 구현한 싱글톤 클래스를 직렬화 하기 위해서는 Serializable을 implements해야 하며 싱글톤을 보장받기 위해서는 인스턴스 필드를 transient로 선언해야 하며 readResolve 메소드를 추가해야 한다.
3. 열거형(Enum)싱글톤
```java
public enum Elvis{
    INSTANCE;
    public void leaveTheBuilding(){...}
}
```
이 방법은 가 항목과 기능적으로는 동일하지만 더 간단하며 앞서 나온 가,나 항목과 다르게 직렬화가 자동으로 지원되고 인스턴스가 여러 개 생기지 않도록 보장하는 장점이 있다.
## 요약
싱글톤 구현 시 열거형(Enum) 방법이 가장 좋은 방법이다.

# private 생성자를 사용해서 인스턴스 생성을 못하게 하자

static 메소드와 static 필드만을 모아놓은 클래스를 만들 필요가 종종 있다. 객체 관점의 사고를 저해한다고 비난하는 사람들이 있지만 그럼에도 불구하고 분명 적합한 용도가 있다.
그러한 클래스들은 상속을 통해 서브 클래스로 확장하는 대신 하나의 final 클래스로 메소드를 모아 놓는데 사용된다. 
인스턴스 생성이 무의미 하기 때문에 인스턴스 생성을 못하게 설계되어 있다. 그러나 그런 유틸리티 클래스일지라도 명시적으로 지정한 생성자가 없을 경우 컴파일러가 디폴트 생성자를 만들어준다. 이러한 경우 javadoc 프로그램으로 생성하는 API 문서에도 나타나므로 인스턴스 생성이 가능한 클래스로 오인될 수 있다. 그러므로 생성자 호출을 통한 인스턴스 생성을 방지하고 API 문서에도 나타나지 않도록 할 수 있는 방법이 필요하다.

## 방법
추상 클래스로 만들어 인스턴스 생성을 불가능하게 하려는 것은 잘못됬다. 추상클래스는 서브 클래스를 만들 수 있고 그 서브 클래스는 인스턴스 생성이 가능하다.

인스턴스를 생성할 수 없게 해주는 간단한 이디엄(idiom)이 있다. 디폴트 생성자는 우리가 명시적으로 지정한 생성자가 전혀 없을 때만 자동으로 생성되기 때문에 우리가 private 생성자를 정의하면 인스턴스 생성이 불가능한 클래스를 만들 수 있다.
```java
public class UtilityClass{
    // 디폴트 생성자 방지 private 생성자
    private UtilityClass(){
        throw new AssertionError();
    }
}
```
위에 예제처럼 private 생성자를 만들어서 디폴트 생성자가 생기지 않도록하고 혹시나 내부에서 실수로 생성자를 호출할 수 있으므로 AssertionError 예외를 써주었다.

## 요약
유틸리티 클래스를 만들어야 할 경우 디폴트 생성자가 생기지 않도록 private 생성자를 만들어주고 코드를 통해서 일부러 그렇게 한것인지 구별 시키기 위해 주석을 달아주자