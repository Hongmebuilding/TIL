# JVM

## JVM (Java Virtual Machine)

개발 환경이 달라도 Java 프로그램을 실행시킬 수 있다. 자바 가상 기기(JVM)가 존재하기 때문이다. JVM이 없으면 디바이스별로 설정해줘야 하는 애로사항이 있다.

### 바이트 코드 (Byte Code)

컴파일러가 OS가 읽을 수 있게 변환한 코드(*.class)

### 인터프리터 (Interpreter)

OS가 읽은 바이트 코드를 디바이스가 실행할 수 있는 기계어로 번역

### JIT (Just In Time)

인터프리터의 속도를 높여주는 서포터

### 메모리 영역

JVM이 OS에게 할당받은 메모리 영역

### 클래스 로더 (Class Loader)

바이트 코드를 메모리 영역으로 운반하는 역할

### 가비지 콜렉터 (Garbage Collector)

메모리 영역에서 사용하지 않는 데이터를 주기적으로 정리하는 청소기

![[Untitled (1).png]]

## JRE (Java Runtime Environment)

자바 실행 환경으로, JVM을 개발자가 구성해주어야 하는데 그때 JRE를 설치함으로써 해결한다.

## JDK (Java Development Kit)

자바 개발 키트로 .java 파일들을 .class 파일들로 변환해주는 Java Compiler(javac) 기능이 있다. 주로 JRE에 포함되어 있다. 디버깅 기능도 있다.