![[Pasted image 20240623190907.png]]


## SOLID 란?

* 객체지향 개발 5대원리, 소프트웨어 개발에서 코드의 유지보수성, 확장성, 재사용성을 높이기 위해 고안된 원칙, SOLID 는 아래의 5가지 원칙으로 구성됨.





### 1. Single Responsibility Principle(SRP)

* 하나의 클래스는 하나의 책임만 가져야 하며, 클래스는 변경할 이유가 하나만 있어한다는 원칙

**예시**
```java
// 잘못된 예시
class Employee {
    public void calculatePay() {
        // 급여 계산 로직
    }
    
    public void saveToDatabase() {
        // 데이터베이스 저장 로직
    }
}

// SRP 적용
class PayCalculator {
    public void calculatePay(Employee employee) {
        // 급여 계산 로직
    }
}

class EmployeeRepository {
    public void saveToDatabase(Employee employee) {
        // 데이터베이스 저장 로직
    }
}

```

➡️ 급여 계산과 데이터베이스 저장이라는 두 가지 다른 책임을 가진 `Employee` 클래스를 두 개의 클래스로 분리하여 각각의 책임을 따로 관리함.




### 2. Open / Closed Principle(OCP)

* 클래스는 확장에는 열려 있어야 하고, 변경에는 닫혀 있어야 한다는 원칙

**예시**
```java
// 잘못된 예시
class Rectangle {
    public double width;
    public double height;
}

class AreaCalculator {
    public double calculateRectangleArea(Rectangle rectangle) {
        return rectangle.width * rectangle.height;
    }
}

// OCP 적용
interface Shape {
    double calculateArea();
}

class Rectangle implements Shape {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
}

class Circle implements Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.calculateArea();
    }
}
```

➡️ 새로운 도형이 추가될 때 `AreaCalculator` 클래스를 수정하지 않고, `Shape` 인터페이스를 구현한 새로운 클래스를 추가하여 기능을 확장할 수 있음.


### 3. Liskov Substitution Principle(LSP)

* 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있어야 한다는 원칙

```java
// 잘못된 예시
class Bird {
    public void fly() {
        // 비행 로직
    }
}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("타조는 날 수 없습니다");
    }
}

// LSP 적용
abstract class Bird {
    public abstract void move();
}

class FlyingBird extends Bird {
    @Override
    public void move() {
        fly();
    }
    
    public void fly() {
        // 비행 로직
    }
}

class Ostrich extends Bird {
    @Override
    public void move() {
        walk();
    }
    
    public void walk() {
        // 걷기 로직
    }
}
```

➡️ `Bird` 클래스의 하위 클래스인 `Ostrich` 가 부모 클래스의 `fly` 메서드를 오버라이드 하지 않도록 구조를 변경하여 `Bird` 클래스가 언제나 자식 클래스로 대체될 수 있도록 함.



### 4. Interface Segregation Principle(ISP)

* 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다는 원칙
```java
// 잘못된 예시
interface Worker {
    void work();
    void eat();
}

// ISP 적용
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Employee implements Workable, Eatable {
    @Override
    public void work() {
        // 업무 수행 로직
    }

    @Override
    public void eat() {
        // 식사 로직
    }
}

class Robot implements Workable {
    @Override
    public void work() {
        // 로봇 업무 수행 로직
    }
}
```

➡️ 로봇은 `eat` 메서드를 필요로 하지 않기 때문에 `Worker` 인터페이스를 `Workable` 과 `Eatable` 로 분리하여 로봇과 인간 직원 모두 필요한 인터페이스만 구현하도록 함.


### 5. Dependency Inversion Principle(DIP)

* 고수준 모듈은 저수준 모듈에 의존해서는 안 되며, 둘 다 추상화에 의존해야 한다는 원칙

```java
// 잘못된 예시
class LightBulb {
    public void turnOn() {
        // 전구 켜기 로직
    }
}

class Switch {
    private LightBulb lightBulb;
    
    public Switch(LightBulb lightBulb) {
        this.lightBulb = lightBulb;
    }
    
    public void operate() {
        lightBulb.turnOn();
    }
}

// DIP 적용
interface Switchable {
    void turnOn();
}

class LightBulb implements Switchable {
    @Override
    public void turnOn() {
        // 전구 켜기 로직
    }
}

class Switch {
    private Switchable device;
    
    public Switch(Switchable device) {
        this.device = device;
    }
    
    public void operate() {
        device.turnOn();
    }
}
```

➡️ `Switch` 클래스가 `LightBulb` 와 같은 구체적인 클래스에 의존하지 않고, `Switchable` 인터페이스에 의존하도록 하여, 다양한 종류의 전기 기기를 사용할 수 있도록 함.


이와 같이 SOLID 원칙을 적용하면 코드의 유연성, 유지보수성, 확장성이 크게 향상됨.