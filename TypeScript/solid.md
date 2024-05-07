# 추상 클래스
### 추상 클래스란?
- 추상 클래스는 클래스와는 다르게 인스턴스화를 할 수 없는 클래스(재사용 불가)이다.
- 상속을 통해 자식 클래스에서 메서드를 제각각 구현하도록 강제하는 용도 -> 핵심 기능의 구현을 전부 자식 클래스에게 위임하고자 한다.
- 예시

```javascript
abstract class Shape {
  abstract getArea(): number; // 추상 함수 정의!!!

  printArea() {
    console.log(`도형 넓이: ${this.getArea()}`);
  }
}

class Circle extends Shape {
  radius: number;

  constructor(radius: number) {
    super();
    this.radius = radius;
  }

  getArea(): number { // 원의 넓이를 구하는 공식은 파이 X 반지름 X 반지름
    return Math.PI * this.radius * this.radius;
  }
}

class Rectangle extends Shape {
  width: number;
  height: number;

  constructor(width: number, height: number) {
    super();
    this.width = width;
    this.height = height;
  }

  getArea(): number { // 사각형의 넓이를 구하는 공식은 가로 X 세로
    return this.width * this.height;
  }
}

const circle = new Circle(5);
circle.printArea();

const rectangle = new Rectangle(4, 6);
rectangle.printArea();
```

# 인터페이스
## 인터페이스란?
- 객체가 가져야 하는 속성과 메서드를 정의한다.

|제목|추상 클래스|인터페이스|
|---|---|---|
|구현부 제공 여부|클래스의 기본 구현을 제공|객체의 구조만을 정의|
|상속 메커니즘|단일 상속만 지원|다중 상속을 지원, 하나의 클래스는 여러 인터페이스를 구현 가능|
|구현 메커니즘|자식 클래스는 반드시 추상 함수를 구현| 정의된 모든 메서드를 전부 구현|
|언제 쓰면 좋을까|기본 구현을 제공하고 상속을 통해 확장|특정 구조를 준수하도록 강제|

# 객체 지향 설계 원칙 SOLID
- 1) S(SRP. 단일 책임 원칙) → ⭐ 매우 중요 ⭐
    
    ### ☑️ SRP 원칙
    
    - 클래스는 **하나의 책임**만 가져야 한다는 매우 기본적인 원칙입니다.
    - 특히, 5개의 설계 원칙 중 **가장 기본적이고 중요한 원칙**이에요! **절대 잊어버리시면 안됩니다!**
    - 예를 들어서, 유저 서비스라는 클래스가 있다고 가정을 해보죠.
    - 이 유저 서비스에서는 유저 관련된 액션만 해야되고 다른 액션을 해서는 안됩니다.
    
    ### ☑️ 잘못된 사례 살펴보기
    
```tsx
class UserService {
      constructor(private db: Database) {}
    
      getUser(id: number): User {
        // 사용자 조회 로직
        return this.db.findUser(id);
      }
    
      saveUser(user: User): void {
        // 사용자 저장 로직
        this.db.saveUser(user);
      }
    
      sendWelcomeEmail(user: User): void {
        // 갑분 이메일 전송 로직이 여기 왜?
        const emailService = new EmailService();
        emailService.sendWelcomeEmail(user);
      }
}
```
    
### ☑️ 올바른 사례 살펴보기
    
```tsx
class UserService {
      constructor(private db: Database) {}
    
      getUser(id: number): User {
        // 사용자 조회 로직
        return this.db.findUser(id);
      }
    
      saveUser(user: User): void {
        // 사용자 저장 로직
        this.db.saveUser(user);
      }
    }
    
    class EmailService {
      // 이메일 관련된 기능은 이메일 서비스에서 총괄하는게 맞습니다.
      // 다른 서비스에서 이메일 관련된 기능을 쓴다는 것은 영역을 침범하는 것이에요!
      sendWelcomeEmail(user: User): void {
        // 이메일 전송 로직
        console.log(`Sending welcome email to ${user.email}`);
      }
}   
```
    
- 2) O(OCP. 개방 폐쇄 원칙) → 인터페이스 혹은 상속을 잘 쓰자!
    - 클래스는 확장에 대해서는 열려 있어야 하고 수정에 대해서는 닫혀 있어야 한다는 원칙입니다.
    - 클래스의 **기존 코드를 변경하지 않고도 기능을 확장**할 수 있어야 합니다.
    - 즉, `인터페이스`나 `상속`을 통해서 이를 해결할 수가 있어요!
        - 부모 클래스의 기존 코드 변경을 하지 않고 기능을 확장하는데 아무런 문제가 없으니까요!
- 3) L(LSP. 리스코프 치환 원칙)
    
    ### ☑️ LSP 원칙
    
    - **서브타입은 기반이 되는 슈퍼타입을 대체**할 수 있어야 한다는 원칙입니다.
    - 다시 말해, 자식 클래스는 부모 클래스의 기능을 수정하지 않고도 부모 클래스와 호환되어야 합니다.
    - 다시 말해서, **논리적으로 엄격하게 관계가 정립**이 되어야 한다는 얘기입니다.
    
    ### ☑️ 잘못된 사례 살펴보기
    
```tsx
class Bird {
      fly(): void {
        console.log("펄럭펄럭~");
      }
    }
    
    class Penguin extends Bird {
      // 으잉? 펭귄이 날 수 있나요? 펭귄이 펄럭펄럭~ 한다는 것은 명백한 위반이죠.
}    
```
    
### ☑️ 올바른 사례 살펴보기
    
```tsx
abstract class Bird {
      abstract move(): void;
    }
    
    class FlyingBird extends Bird {
      move() {
        console.log("펄럭펄럭~");
      }
    }
    
    class NonFlyingBird extends Bird {
       move() {
        console.log("뚜벅뚜벅!");
      }
}
    
class Penguin extends NonFlyingBird {} // 이제 위배되는 것은 아무것도 없네요!    
```
    
- 4)  I(ISP. 인터페이스 분리 원칙)
    - 클래스는 자신이 사용하지 않는 인터페이스의 영향을 받지 않아야 합니다.
    - 즉, **해당 클래스에게 무의미한 메소드의 구현을 막자**는 의미에요!
    - 따라서, **인터페이스를** 너무 크게 정의하기보단 **필요한 만큼만 정의**하고 **클래스는 입맛에 맞게 필요한 인터페이스들을 구현**하도록 유도합니다!
- 5) D(DIP. 의존성 역전 원칙)
    
    ### ☑️ DIP 원칙
    
    - DIP는 Java의 Spring 프레임워크나 Node.js의 Nest.js 프레임워크와 같이 **웹 서버 프레임워크 내에서 많이 나오는 원칙**이에요.
    - 이 원칙은 하위 수준 모듈(구현 클래스)보다 **상위 수준 모듈(인터페이스)에 의존**을 해야한다는 의미입니다!
    - 예를 들어서, 데이터베이스라는 클래스가 있다고 가정을 해보겠습니다.
    - 데이터베이스의 원천은 로컬 스토리지가 될 수도 있고 클라우드 스토리지가 될 수도 있어요.
    - 이 때, 데이터베이스의 원천을 로컬 스토리지 타입 혹은 클라우드 스토리지 타입으로 한정하는 것이 아닙니다.
    - 그보다 상위 수준인 스토리지 타입으로 한정을 하는 것이 맞아요!
    
    ### ☑️ 사용 사례
    
```tsx
interface MyStorage {
      save(data: string): void;
    }
    
    class MyLocalStorage implements MyStorage {
      save(data: string): void {
        console.log(`로컬에 저장: ${data}`);
      }
    }
    
    class MyCloudStorage implements MyStorage {
      save(data: string): void {
        console.log(`클라우드에 저장: ${data}`);
      }
    }
    
    class Database {
      // 상위 수준 모듈인 MyStorage 타입을 의존! 
      // 여기서 MyLocalStorage, MyCloudStorage 같은 하위 수준 모듈에 의존하지 않는게 핵심!
      constructor(private storage: MyStorage) {}
    
      saveData(data: string): void {
        this.storage.save(data);
      }
}
    
const myLocalStorage = new MyLocalStorage();
const myCloudStorage = new MyCloudStorage();
   
const myLocalDatabase = new Database(myLocalStorage);
const myCloudDatabase = new Database(myCloudStorage);
    
myLocalDatabase.saveData("로컬 데이터");
myCloudDatabase.saveData("클라우드 데이터");    
```