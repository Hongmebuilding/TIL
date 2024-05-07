# mini project
## 별다방 프로그램 만들기
- 별다방 프로그램 코딩 - 인터페이스 & 데이터 정의하기!
 - **[코드] 유저 인터페이스 정의**
            
```tsx
    interface User {
              id: number;
              name: string;
              role: 'admin' | 'customer';
    }        
```
- **[코드] 음료 인터페이스 정의**
            
```tsx
    interface Beverage {
              name: string;
              price: number;
    }        
```
- **[코드] 주문 인터페이스 정의**
            
```tsx
    interface Order {
              orderId: number;
              customerId: number;
              customerName: string;
              beverageName: string;
              status: "placed" | "completed" | "picked-up";
    }        
```
- **[코드] 데이터 정의**
            
```tsx
    let beverages: Beverage[] = [];
    let orders: Order[] = [];        
```
			
### > 고객인지 어드민인지 체크하는 함수 만들기   
<details>
  <summary>답안</summary>
- [코드] 어드민 권한 체크 함수
            
```tsx
 function isAdmin(user: User): boolean {
              return user.role === "admin";
            }
```
 
-[코드] 고객 권한 체크 함수
            
```tsx
function isCustomer(user: User): boolean {
    return user.role === "customer";
}
 ```
</details>

### > 다음으로는 음료 목록에 음료를 새롭게 등록하는 addBevearage라는 함수를 만들자. 이 함수의 시그니처는 다음과 같다. 또한, 이 함수는 어드민만 호가능하다.
```javascript
function addBeverage(user: User, name: string, price: number): void { ... }
```
<details>
  <summary>답안</summary>
- [코드] 음료 등록 기능 - 어드민

```tsx
function addBeverage(user: User, name: string, price: number): void {
    if (!isAdmin(user)) {
        console.log("권한이 없습니다.");
        return;
    }
            
    const newBeverage: Beverage = { name, price };
    beverages.push(newBeverage);
}
```
</details>

### > 음료 목록에서 음료를 삭제하는 removeBeverage라는 함수를 만들자.  이 함수의 시그니처는 다음과 같다. 마찬가지로, 이 함수도 어드민만 호출 가능하다.
```javascript
function removeBeverage(user: User, beverageName: string): void { ... }
```
<details>
  <summary>답안</summary>
- [코드] 음료 삭제 기능 - 어드민

```javascript
 function removeBeverage(user: User, beverageName: string): void {
    if (!isAdmin(user)) {
        console.log("권한이 없습니다.");
        return;
    }
            
    beverages = beverages.filter((beverage) => beverage.name !== beverageName);
}
```
</details>

### > 어드민 혹은 고객이면 볼 수 있는 음료 목록
```javascript
function removeBeverage(user: User, beverageName: string): void { ... }
```
<details>
  <summary>답안</summary>
- [코드] 음료 조회 기능 - 어드민, 고객

```tsx
    function getBeverages(user: User): Beverage[] {
        if (!user) {
        return [];
        }
        return beverages;
     }
```
</details>

### > 고객이 음료 주문을 할 때 판매하지 않는 음료를 사는 것을 막기 위한 음료 찾기 함수 만들기
- [코드] 음료 찾기 함수

```javascript
    function findBeverage(beverageName: string): Beverage | undefined {
        return beverages.find((beverage) => beverage.name === beverageName);
    }
```
<details>
  <summary>답안</summary>

```tsx
    
    function findBeverage(beverageName: string): Beverage | undefined {
        return beverages.find((beverage) => beverage.name === beverageName);
    }
```
</details>
     
- [코드] 음료 주문 기능 - 고객
            
### > 음료 주문 기능 placeOrder라는 함수를 만들자. 이 함수의 시그니처는 다음과 같다. 이 함수는 고객만 호출 가능하고 엉뚱한 커피 주문은 막아야 하고, 주문 ID를 리턴해야 한다.

```tsx
function placeOrder(user: User, beverageName: string): number { ... }
```

<details>
  <summary>답안</summary>

```tsx
    function placeOrder(user: User, beverageName: string): number {
              if (!isCustomer(user)) {
                console.log("권한이 없습니다.");
                return -1;
              }
            
              const beverage = findBeverage(beverageName);
              if (!beverage) {
                console.log("해당 음료를 찾을 수 없습니다.");
                return -1;
              }
            
              const newOrder: Order = {
                orderId: orders.length + 1,
                customerId: user.id,
                customerName: user.name,
                beverageName,
                status: "placed",
              };
              orders.push(newOrder);
              return newOrder.orderId;
    }        
``` 
</details>      
            
- [코드] 음료 준비 완료 기능 - 어드민
  
### > 고객이 주문한 음료가 준비가 완료되었다는 동작을 담당하는 completeOrder라는 함수를 만들자. 이 함수의 시그니처는 다음과 같고 이 함수는 어드민만 부를 수 있다.

```tsx
function completeOrder(user: User, orderId: number): void { ... }
```
            
<details>
  <summary>답안</summary>

```tsx
   function completeOrder(user: User, orderId: number): void {
              if (!isAdmin(user)) {
                console.log("권한이 없습니다.");
                return;
              }
            
              const order = orders.find((order) => order.orderId === orderId);
              if (order) {
                order.status = "completed"; // 단순히 주문의 상태만 바꾸고 끝!
                console.log(
                  `[고객 메시지] ${order.customerName}님~ 주문하신 ${order.beverageName} 1잔 나왔습니다~`
                );
              }
            }         
 ```
 </details>

### > 마지막으로 음료 수령하는 기능을 만들자.

- [코드] 음료 수령 기능 - 고객

<details>
  <summary>답안</summary>
  
```tsx
   function pickUpOrder(user: User, orderId: number): void {
              if (!isCustomer(user)) {
                console.log("권한이 없습니다.");
                return;
              }
            
              const order = orders.find(
                (order) => order.orderId === orderId && order.customerId === user.id
              );
              if (order && order.status === "completed") {
                order.status = "picked-up";
                console.log(
                  `[어드민 메시지] 고객 ID[${order.customerId}]님이 주문 ID[${orderId}]을 수령했습니다.`
                );
              }
    }         
```
 </details>            
    
### > 별다방 프로그램 코딩 - 테스트 코드를 포함한 전체 코드
    
<details>
  <summary>답안</summary>

    ```tsx
    interface Beverage {
      name: string;
      price: number;
    }
    
    interface User {
      id: number;
      name: string;
      role: "admin" | "customer";
    }
    
    interface Order {
      orderId: number;
      customerId: number;
      customerName: string;
      beverageName: string;
      status: "placed" | "completed" | "picked-up";
    }
    
    let beverages: Beverage[] = [];
    let orders: Order[] = [];
    
    function isAdmin(user: User): boolean {
      return user.role === "admin";
    }
    
    function isCustomer(user: User): boolean {
      return user.role === "customer";
    }
    
    function addBeverage(user: User, name: string, price: number): void {
      if (!isAdmin(user)) {
        console.log("권한이 없습니다.");
        return;
      }
    
      const newBeverage: Beverage = { name, price };
      beverages.push(newBeverage);
    }
    
    function removeBeverage(user: User, beverageName: string): void {
      if (!isAdmin(user)) {
        console.log("권한이 없습니다.");
        return;
      }
    
      beverages = beverages.filter((beverage) => beverage.name !== beverageName);
    }
    
    function getBeverages(user: User): Beverage[] {
      if (!user) {
        return [];
      }
      return beverages;
    }
    
    function findBeverage(beverageName: string): Beverage | undefined {
      return beverages.find((beverage) => beverage.name === beverageName);
    }
    
    function placeOrder(user: User, beverageName: string): number {
      if (!isCustomer(user)) {
        console.log("권한이 없습니다.");
        return -1;
      }
    
      const beverage = findBeverage(beverageName);
      if (!beverage) {
        console.log("해당 음료를 찾을 수 없습니다.");
        return -1;
      }
    
      const newOrder: Order = {
        orderId: orders.length + 1,
        customerId: user.id,
        customerName: user.name,
        beverageName,
        status: "placed",
      };
      orders.push(newOrder);
      return newOrder.orderId;
    }
    
    function completeOrder(user: User, orderId: number): void {
      if (!isAdmin(user)) {
        console.log("권한이 없습니다.");
        return;
      }
    
      const order = orders.find((order) => order.orderId === orderId);
      if (order) {
        order.status = "completed";
        console.log(
          `[고객 메시지] ${order.customerName}님~ 주문하신 ${order.beverageName} 1잔 나왔습니다~`
        );
      }
    }
    
    function pickUpOrder(user: User, orderId: number): void {
      if (!isCustomer(user)) {
        console.log("권한이 없습니다.");
        return;
      }
    
      const order = orders.find(
        (order) => order.orderId === orderId && order.customerId === user.id
      );
      if (order && order.status === "completed") {
        order.status = "picked-up";
        console.log(
          `[어드민 메시지] 고객 ID[${order.customerId}]님이 주문 ID[${orderId}]을 수령했습니다.`
        );
      }
    }
    
    function main() {
      const admin: User = {
        id: 1,
        name: "바리스타",
        role: "admin",
      };
    
      // 유저 생성
      const member1: User = {
        id: 2,
        name: "르탄이",
        role: "customer",
      };
    
      const member2: User = {
        id: 3,
        name: "꿈꾸는개발자",
        role: "customer",
      };
    
      // 음료 등록
      addBeverage(admin, "아메리카노", 4000);
      addBeverage(admin, "카페라떼", 4500);
      addBeverage(admin, "에스프레소", 3000);
    
      // 음료 삭제
      removeBeverage(admin, "에스프레소");
    
      console.log(
        `안녕하세요~ ${
          member1.name
        } 고객님! 별다방에 오신 것을 환영합니다. 저희는 ${JSON.stringify(
          getBeverages(member1)
        )}를 판매하고 있습니다.`
      );
      // 음료 주문
      const orderId1 = placeOrder(member1, "아메리카노");
      if (orderId1 > 0) {
        setTimeout(() => {
          // 음료 제작 완료
          completeOrder(admin, orderId1);
          // 음료 수령
          pickUpOrder(member1, orderId1);
        }, 1000);
      }
    
      console.log(
        `안녕하세요~ ${
          member2.name
        } 고객님! 별다방에 오신 것을 환영합니다. 저희는 ${JSON.stringify(
          getBeverages(member2)
        )}를 판매하고 있습니다.`
      );
      // 음료 주문
      const orderId2 = placeOrder(member2, "카페라떼");
      if (orderId2 > 0) {
        setTimeout(() => {
          // 음료 제작 완료
          completeOrder(admin, orderId2);
          // 음료 수령
          pickUpOrder(member2, orderId2);
        }, 3000);
      }
    }
    
    main();
    ```
</details> 