# mini project
## 도서관 만들기

> Role이라는 enum을 정의해보자.
        
- **[코드] 역할 enum**
 ```tsx
enum Role {
  LIBRARIAN, // 사서
  MEMBER, // 멤버
}
 ```

> User라는 추상 클래스를 정의해보자.<br> User 클래스는 name, age라는 인자를 받고 getRole이라는 추상 함수를 포함한다.

- **[코드] 유저 추상 클래스**

```tsx
abstract class User {
  constructor(public name: string, public age:  number) {}
  abstract getRole(): Role;
}
```

> Member라는 클래스를 정의해보자. Member는 User를 상속받는다.

- **[코드] 멤버 클래스**

 ```tsx
class Member extends User {
  constructor(name: string, age: number) {
    super(name, age);
  }
  getRole(): Role {
     return Role.MEMBER;
  }
}
 ```

>마찬가지로 Librarian라는 클래스를 정의해보자.

- **[코드] 사서 클래스**

```tsx
class Librarian extends User {
  constructor(name: string, age: number) {
    super(name, age);
  }
  getRole(): Role {
    return Role.LIBRARIAN;
  }
}
```
            
>이제 Book이라는 클래스를 정의해보자.<br> 책은 `이름`, `저자`, `출판일`로 구성이 된다.

- **[코드] 책 클래스**

```tsx
class Book {
  constructor(
    public title: string,
    public author: string,
    public publishedDate: Date
  ) {}
}
```

> RentManager라는 인터페이스를 정의해볼게요.<br> 이 친구는 도서관이 꼭 갖추어야 할 기능을 정의한 명세서입니다.

- **[코드] RentManager 인터페이스**

 ```tsx
interface RentManager {
  getBooks(): Book[];
  addBook(user: User, book: Book): void;
  removeBook(user: User, book: Book): void;
  rentBook(user: Member, book: Book): void;
  returnBook(user: Member, book: Book): void;
}
```

> 이제, RentManager를 구현하는 Library 클래스를 만들어보자. <br>
        - getBooks 함수는 books를 깊은 복사해서 던져주자.<br>
            - 외부에서 books를 수정하는 것을 방지하기 위함<br>
        - addBook, removeBook는 사서만 호출할 수 있게 해주자.<br>
        - rentBook는 유저만 호출 할 수 있게 해준다.<br>
        - rentBook에서는 다른 책을 대여한 유저는 책을 대여할 수 없어야 한다.<br>
        - returnBook에서는 책을 빌린 사람들만 반납할 수 있게 해준다.

- **[코드] 도서관 클래스 구현**
```tsx
  class Library implements RentManager {
    private books: Book[] = [];// rentedBooks는 유저의 대여 이력을 관리
    private rentedBooks: Map<string, Book> = new Map<string, Book>();
    getBooks(): Book[] {// 깊은 복사를 하여 외부에서 books를 수정하는 것을 방지
    return JSON.parse(JSON.stringify(this.books));
    }
            
    addBook(user: User, book: Book): void {
      if (user.getRole() !== Role.LIBRARIAN) {
        console.log("사서만 도서를 추가할 수 있습니다.");
        return;
      }
            
      this.books.push(book);
    }
            
    removeBook(user: User, book: Book): void {
      if (user.getRole() !== Role.LIBRARIAN) {
      console.log("사서만 도서를 삭제할 수 있습니다.");
     return;
    }
            
    const index = this.books.indexOf(book);
      if (index !== -1) {
        this.books.splice(index, 1);
      }
    }
            
    rentBook(user: User, book: Book): void {
      if (user.getRole() !== Role.MEMBER) {
      console.log("유저만 도서를 대여할 수 있습니다.");
      return;
    }
            
    if (this.rentedBooks.has(user.name)) {
      console.log(
       `${user.name}님은 이미 다른 책을 대여중이라 빌릴 수 없습니다.`
      );
    } else {
       this.rentedBooks.set(user.name, book);
       console.log(`${user.name}님이 [${book.title}] 책을 빌렸습니다.`);
    }
}
            
    returnBook(user: User, book: Book): void {
      if (user.getRole() !== Role.MEMBER) {
      console.log("유저만 도서를 반납할 수 있습니다.");
      return;
     }
            
                if (this.rentedBooks.get(user.name) === book) {
                  this.rentedBooks.delete(user.name);
                  console.log(`${user.name}님이 [${book.title}] 책을 반납했어요!`);
                } else {
                  console.log(`${user.name}님은 [${book.title}] 책을 빌린적이 없어요!`);
                }
              }
            }
```          
    
> 도서관 프로그램 코딩 - 테스트 코드를 포함한 전체 코드

```tsx
enum Role {
  LIBRARIAN,
  MEMBER,
}
    
abstract class User {
  constructor(public name: string, public age: number) {}
  abstract getRole(): Role;
}
    
class Member extends User {
   constructor(name: string, age: number) {
     super(name, age);
   }
   getRole(): Role {
     return Role.MEMBER;
   }
}
    
class Librarian extends User {
  constructor(name: string, age: number) {
    super(name, age);
  }
  getRole(): Role {
    return Role.LIBRARIAN;
  }
}
    
class Book {
  constructor(
    public title: string,
    public author: string,
    public publishedDate: Date
  ) {}
}
    
interface RentManager {
  getBooks(): Book[];
  addBook(user: User, book: Book): void;
  removeBook(user: User, book: Book): void;
      rentBook(user: Member, book: Book): void;
      returnBook(user: Member, book: Book): void;
  }
    
  class Library implements RentManager {
    private books: Book[] = [];
    private rentedBooks: Map<string, Book> = new Map<string, Book>();
    
    getBooks(): Book[] {
    // 깊은 복사를 하여 외부에서 books를 수정하는 것을 방지합니다.
      return JSON.parse(JSON.stringify(this.books));
    }
    
    addBook(user: User, book: Book): void {
      if (user.getRole() !== Role.LIBRARIAN) {
        console.log("사서만 도서를 추가할 수 있습니다.");
        return;
      }
    
      this.books.push(book);
    }
    
      removeBook(user: User, book: Book): void {
        if (user.getRole() !== Role.LIBRARIAN) {
          console.log("사서만 도서를 삭제할 수 있습니다.");
          return;
        }
    
        const index = this.books.indexOf(book);
        if (index !== -1) {
          this.books.splice(index, 1);
        }
      }
    
      rentBook(user: User, book: Book): void {
        if (user.getRole() !== Role.MEMBER) {
          console.log("유저만 도서를 대여할 수 있습니다.");
          return;
        }
    
        if (this.rentedBooks.has(user.name)) {
          console.log(
            `${user.name}님은 이미 다른 책을 대여중이라 빌릴 수 없습니다.`
          );
        } else {
          this.rentedBooks.set(user.name, book);
          console.log(`${user.name}님이 [${book.title}] 책을 빌렸습니다.`);
        }
      }
    
      returnBook(user: User, book: Book): void {
        if (user.getRole() !== Role.MEMBER) {
          console.log("유저만 도서를 반납할 수 있습니다.");
          return;
        }
    
        if (this.rentedBooks.get(user.name) === book) {
          this.rentedBooks.delete(user.name);
          console.log(`${user.name}님이 [${book.title}] 책을 반납했어요!`);
        } else {
          console.log(`${user.name}님은 [${book.title}] 책을 빌린적이 없어요!`);
        }
      }
    }
    
    function main() {
      const myLibrary = new Library();
      const librarian = new Librarian("르탄이", 30);
      const member1 = new Member("예비개발자", 30);
      const member2 = new Member("독서광", 28);
    
      const book = new Book("TypeScript 문법 종합반", "강창민", new Date());
      const book2 = new Book("금쪽이 훈육하기", "오은영", new Date());
      const book3 = new Book("요식업은 이렇게!", "백종원", new Date());
    
      myLibrary.addBook(librarian, book);
      myLibrary.addBook(librarian, book2);
      myLibrary.addBook(librarian, book3);
      const books = myLibrary.getBooks();
      console.log("대여할 수 있는 도서 목록:", books);
    
      myLibrary.rentBook(member1, book);
      myLibrary.rentBook(member2, book2);
    
      myLibrary.returnBook(member1, book);
      myLibrary.returnBook(member2, book2);
    }
    
    main();
```