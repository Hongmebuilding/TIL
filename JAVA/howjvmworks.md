# JVM
## JVM의 구조
참고문현 : https://www.youtube.com/watch?v=GU254H0N93Y
자바.java라는 파일이 jvm을 어떻게 거치는지에 대해 설명해보겠다.
1. Class loader Systemdl Runtime Data Areas 로 넘긴다.
2. Runtime Data Areas
	1) Method Area : class 정보를 저장
	2) Heap : Object 정보를 저장한다. JVM이 객체를 위해 필요한 Heap 공간의 크기를 결정하면 Heap 공간을 할당하고 인스턴스 변수값을 초기 값으로 초기화 한다.
	3) JVM Stacks : Frame 정보로 구성. JVM이 main 메서드의 명령을 Stacks에 push한다.
		Frame은 method가 하나 호출될때 자료구조 stack 처럼 쌓인다. 
			1. Local Variables Array : method 내의 지역변수 명칭을 저장한다.
			2. Operand Stack : 피연산자를 저장한다.
			3. 상수 pool 참조 : 상수값들을 저장한다.
	4) PC Registers : 현재 실행되고 있는 명령어의 주소를 저장하는 것이다. multi thread 환경에서 현재 어떤 명령어를 실행해야 할지 기억해야할 때 사용된다.
	5) Native Method Statcks : c나 c++로 작성된 메소드를 실행할 때 사용된다.
	- 3),4),5)의 영역은 thread마다 각각 생긴다.