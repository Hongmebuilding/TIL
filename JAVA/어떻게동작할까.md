# 어떻게 동작할까
```java
public class Main {
	public static void main(String[] args) {
		System.out.println("haha")
	}
}
```
1. 우리는 Main.java 파일을 만든다. 그럼 class Main이라는 명칭이 주어지는데 compiler는 이 class라는 키워드를 기반으로 Main이라는 class를 만든다. 
2. class loder가 메모리 영역으로 실어 나른다.

### main method
jvm의 약속 중 모든 자바 프로젝트는 제일 먼저 클래스의 main 메소드를 실행시킨다.

##### 클래스 로더가 Main.java 파일을 메모리로 로드한 후, 바이트코드는 JVM(Java Virtual Machine) 메모리 영역에 다음과 같이 적재된다

- 메서드 영역(Method Area)
클래스 정보(클래스 이름, 상위 클래스, 구현한 인터페이스 등)
필드 정보(인스턴스 변수, 클래스 변수 등)
메서드 정보(메서드 이름, 매개변수, 리턴 타입 등)
상수 풀(문자열 리터럴, 숫자 리터럴 등)

- 스택 영역(Stack Area)
메서드 호출 시 프레임이 생성되고, 이 프레임에는 로컬 변수와 메서드 호출 정보가 저장된다.
main 메서드가 호출되면 main 메서드의 프레임이 스택에 푸시한다.

- 힙 영역(Heap Area)
객체와 배열이 생성되는 영역이다.
System.out.println("haha") 문장에서 "haha" 문자열 객체가 힙 영역에 생성된다.

JVM 메모리 구조
![memory](https://github.com/Hongmebuilding/TIL/assets/87316411/77c43ae0-9e53-4aa5-894d-f0ee2548cabc)

                     바이트코드 실행 순서
1. Main 클래스 로드
2. main 메서드 호출 및 프레임 푸시
3. "haha" 문자열 객체 생성
4. println 메서드 호출 및 프레임 푸시
5. "haha" 문자열 출력
6. println 메서드 프레임 팝
7. main 메서드 프레임 팝 및 프로그램 종료
