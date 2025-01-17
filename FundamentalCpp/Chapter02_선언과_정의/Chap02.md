# Chapter 02 선언과 정의
## 2.1 선언과 정의의 구분
### 2.1.1 정의
C++에서 말하는 정의란 바로 객체를 만들겠다는 것
* 객체를 만든다? -> 메모리를 할당하겠다는 것

결국 정의란 어떤 대상이 실제로 존재할 수 있도록 메모리 영역을 만들어주는 작업
* 그러나 클래스의 경우 정의 개념이 조금 달라진다.

클래스 정의란 이 클래스가 어떻게 구성되었는지 나타내는 설계도
* 설계도 또한 메모리를 차지한다. 

기존 변수들은 프로세스가 사용하는 가상 메모리를 나타냄

클래스의 설계도가 저장되는 메모리는 프로세스와 상관없이 컴파일러가 사용하는 메모리

* 클래스 멤버 객체가 선언
  * 클래스 객체가 생성되어 객체에 대한 메모리가 할당될 경우 할당된 영역의 특정 부분이 멤버 객체에게 할당된다는 것을 의미
* 클래스 멤버 함수가 선언
  * 해당 함수가 멤버 함수임을 알림
* 클래스 멤버 함수가 정의
  * 프로세스가 시작될 경우 함수의 본체가 코드 영역의 메모리를 차지

간단히 정리하면, 어떤 대상이 존재할 수 있도록 메모리를 할당하는 것이 정의
* 일반적인 객체와 함수가 정의에 의해서 할당되는 메모리는 가상 메모리
* 클래스가 정의에 의해 할당되는 메모리는 컴파일러 메모리

### 2.1.2 선언
선언이란 바로 어떤 객체가 존재하고 있음을 알리는 역할


클래스를 선언한다는 것은 이런 클래스가 있으니 타입으로 사용해도 좋다는 것을 의미

정의와 선언이 뭐가 다르지?
* 정의는 곧 선언을 포함하기 때문
* 그러나 선언이 꼭 필요한 경우가 있다. (파일이 다를 때)

extern 키워드를 사용하면 정의가 아닌 순수한 선언만을 할 수 있다.

여기서 A 파일 B 파일 둘 다 선언하면 안되나?
* 링커 에러 : 중복 정의를 허용하지 않는다.
* 혼란을 피하기 위해


### 2.1.3 extern & static
* extern : 외부의
* static : 정적인
* local : 지역

extern과 static은 local과는 반대되는 속성을 가진다.
* extern과 static은 전역 객체의 특성을 가지지만
* static 객체는 사용 범위가 한정된다는 측면 : 정적 객체로 표현

객체는 local과 비 local로 나누어질 수 있다.

extern과 static의 차이
* static이 다른 파일에 있을 경우 가져올 수 없다.

extern은 정의와 선언 모두 사용할 수 있다.
* extern이 정의에 사용되면 extern이 생략될 수 있다.
* 선언은 생략할 수 없다.
* extern이 정의에 사용되면 어떤 객체의 초기화가 이루어질 수 있다.
* 선언이라면 초기화가 불가능하다.


### 2.1.4 클래스 선언과 정의
* 클래스라는 것은 일종의 설계도 다른 객체와는 성격이 다른것을 의미
* 클래스는 오직 개념적인 구조로 존재한다.

클래스 멤버 변수에 접근하는 것은 클래스 정의에 따라 해당 멤버 변수의 메모리 오프셋에 의해서 계산된 위치를 기준으로 한다.


## 2.2 기억 부류 (Storage Class)

### 2.2.1 논리 공간
* 같은 이름의 전역 변수는 실행 공간에 오직 단 한번만 정의될 수 있다.
* 같은 이름의 static 변수는 각각의 오브젝트 공간에 단 한번만 정의될 수 있다.
* 같은 이름과 같은 인자 타입을 가진 전역함수는 오브젝트 공간에 단 한번만 정의될 수 있다.
* 같은 이름의 클래스는 각각의 오브젝트 공간에 오직 단 한번만 정의될 수 있다.

### 2.2.2 변수 할당과 초기화
정적 변수를 포함한 전역 변수는 프로그램 시작 순간에 메모리를 할당받는다.
* 프로세스가 시작하고 가상 메모리 영역이 설정될 때 데이터 영역에 전역 객체에 대한 영역이 마련되어 있다는 것

지역 변수의 메모리 할당은 함수가 실행되는 시점
* 지역변수가 위치하는 영역은 스레드 스택

가상 메모리 중 코드와 데이터 영역은 순서가 큰 의미가 없다.
* 마찬가지로 지역변수 또한

함수 안에서 사용되는 모든 지역 변수들의 크기를 먼저 구하고 함수 실행 시점에 스택을 늘리기 때문
* call 명령어 전후로 스택이 생성

메모리 할당 순서는 큰 의미가 없지만, 초기화는 순서가 중요하다.


프로세스가 실행 -> 스레드도 실행 -> 스레드가 함수 실행
* 프로세스가 시작되면서 최초 호출하는 시작함수 : CRT Startup
* CRT Startup이 main을 호출하게 된다.
* 물론 CRT Startup은 main이 호출되기 전 많은 작업을 수행함.


상수로 초기화한 전역 변수는 CRT Startup이 호출되기 이전부터 값이 설정되어 있다.
* 메모리 영역이 할당되는 순간에 해당 상수 값으로 초기화한다.

초기화 안한 전역 변수는 CRT Startup이 호출되기 이전에는 모두 0이다.
* BSS 영역에서 가상 메모리로 올라올 때 0으로 초기화가 이루어진다.

전역 변수는 상수로 초기화한 것이 가장 먼저 초기화 값이 설정
* 그 다음으로는 함수의 반환을 통한 초기화
* 함수를 통해 전역 변수를 초기화하는 경우 CRT Startup이 main을 호출하기 전에 먼저 초기화 함수를 호출한다.

지역 변수의 초기화는 코드 순서대로 이뤄진다.


### 2.2.3 변수 초깃값
변수가 정의되어 생성될 경우 변수의 초기값은 어떻게 정해질까?
* 모든 변수가 초기화되면 좋겠지만. 아니다.
* 초기화를 하는데 CPU가 사용되기 때문이다.
* 즉, 변수가 많을수록 효율이 떨어진다.

스택 영역의 지역 변수

int x, y, z;\
x = 1;\
y = 2;\
z = x + y;
1. int x, y, z; : main이 시작되면서 스택에 영역 할당
2. x = 1;, y = 2;, z = x + y; : 값이 정해진다.

* 변수가 선언되는 시점에 z의 값이 정해질 필요가 없다.
* 쓸데없이 CPU를 사용하면서 변수들이 차지한 스택 메모리 영역을 초기화할 필요가 없다.

전역 변수의 초기값

전역 변수

int g_A;\
int g_B = 0;\
int g_C = 1;\
int g_D = GetTwo();
1. 초기화 없는 전역 변수
2. 기본값 초기화 전역 변수
3. 상수 초기화 전역 변수
4. 함수 초기화 전역 변수

가상 메모리의 어느 영역 출신이냐로 나누면 1, 2, 4 - 3 으로 나눌 수 있다.

전역 변수와 정적 변수는 데이터 영역에 위치하게 된다.
* 초기화된 데이터 영역 : Data 영역
* 초기화되지 않은 데이터 영역 : BSS 영역 (Block Stated Symbol)

3번은 1로 초기화된 상태이다.
* 즉, 가상 메모리가 구성되는 시점에 이미 1로 채워지는 것
* 데이터 영역은 0이 아닌 초기화된 전역 변수들이 위치

BSS 영역은 가상 메모리가 구성되는 시점에 모두 0으로 채워지는 영역
* 1, 2 는 BSS 영역에 위치한다.
* 4 또한 가상메모리가 구성이 완료되고 최초의 스레드가 CRT Startup이 초기화 처리 함수를 호출할 때이다.
* 즉, GetTwo가 호출되기 전까지 g_D는 BSS 영역에 위치하므로 0을 가지고 있다.

BSS 영역은 왜 만들었을까?
* 초기화되지 않은 전역 변수를 위해 특별히 고안
* 변수가 생성되는 시점에 초기값을 가지는 것은 안전을 위해 필요하다.
* 지역 변수의 경우 효율을 생각해 그렇게 하지 못하는 것
* 전역 변수의 경우 프로세스 시작 시 딱 한번만 초기화하면 되므로 부담이 없다.
* 따라서 전역 변수는 가장 기본이 되는 0으로 초기화를 진행한다.

BSS 영역을 추가한 이유
* 초기화되지 않은 전역변수를 모아두고
* 한번에 0으로 밀어버리기 위함

각 전역 변수의 주소를 찍어보면

g_A : 00C95184\
g_B : 00C951AC\
g_C : 00C9508C\
g_D : 00C951C0
* 나머지는 비슷비슷한 위치인데
* g_C만 많이 차이난다. : 데이터 영역
* 데이터 영역이 BSS 영역보다 더 작은 주소 방향에 위치한다.

실제 프로젝트에서 최종 바이너리를 만들어야 하는 경우 이런 작은 부분까지 신경써야 한다.
* 전역 변수의 초깃값 여부에 따라서 최종 바이너리 크기가 달라질 수 있기 때문

상수로 초기화된 전역 객체를 바이너리로 만들면 실행 이미지에 초깃값을 모두 기록해야 한다.
* 초기화된 전역 객체의 경우 객체 크기만큼 실행 바이너리도 커진다.

BSS 영역의 전역객체는 실행 이미지에서 값을 알필요가 없다.\
* BSS 영역이 구성될 때 객체 크기만 알고 그 부분을 0으로 밀면 되기 때문에

힙영역 또한 초기화가 일어나지 않는다.
* 빈번하게 할당과 해제가 일어나기 때문


### 2.2.4 디버그 변수 초깃값
VC++ 컴파일러의 디버그 모드에서는 특별히 지역 변수와 힙 할당 메모리 영역을 특정 값으로 초기화를 한다.

지역변수 : cc cc cc cc\
힙 할당 메모리 : cd cd cd cd\
힙 할당 메모리 양 끝 : fd fd fd fd\
해제된 힙 할당 메모리 : dd dd dd dd
* 초깃값은 쉽게 구분 가능하도록 16진수 기준으로 반복적인 문자를 사용
* 버그 상태의 초깃값을 16진수로 출력하려면 cout에 hex 지정


## 2.3 정적 변수
정적 변수의 접근 범위는 세 가지로 나눌 수 있다.
* 소스 파일, 클래스, 함수

1. 소스 파일을 범위로 가지는 정적 변수 : 정적 전역 변수
2. 함수에 사용되는 정적 변수 : 정적 지역 변수

모든 정적 변수는 데이터 영역에 위치하며 프로세스 실행 시점에 상수 또는 기본값으로 초기화


### 2.3.1 정적 전역 변수
정적 전역 변수는 전역 변수 앞에 static을 붙인 것
* cpp 파일에서만 접근 가능하다.

### 2.3.2 정적 멤버 변수
클래스 멤버 변수 앞에 static을 붙인 것
* 클래스 정의에서 정적 멤버 변수를 정의했다고 해서 실제로 정적 멤버 변수가 정의된 것은 아니다.

정적 멤버 변수는 클래스 객체의 할당된 메모리 영역을 사용하지 않는다.
* 실제로는 전역 변수와 똑같다.
* 정적 멤버 변수가 자신만의 메모리 영역에 할당 받기 위해서는 정의를 해주어야만 한다.
* 정의는 어디서? -> 소스 파일에 단 한번만 한다.

정적 멤버 변수는 사실상 멤버 변수가 아니다.
* 클래스 객체의 영향을 받지 않는다.


### 2.3.3 정적 지역 변수
절대로 지역 변수의 성질을 가지는 것이 아니다.
* 함수 안에서만 접근할 수 있는 전역 변수와 같다.
* 즉, 프로세스 시작시에 생성되고 초기화되어 있는 것이다.

정적 지역 변수의 초기화는 전역 변수가 초기화되는 과정과 동일하다.
* 초기화 되지 않으면 BSS
* 초기화 되면 Data

정적 지역 변수는 애초에 함수 선언과는 상관이 없다.
* 이미 프로세스 시작시에 생성되고 초기화되었기 때문

그러나 정적 지역 변수를 함수를 통해서 초기화하는 경우
* 초기화 코드가 어셈블리로 추가된다.
    
~~~
		mov			eax, dword ptr [$S2]    ; $S2 초기화 여부를 기록하는 전역 변수
		and			eax. 1                  ; 1인지 체크
		jne			EXIT

	START:
		mov			eax, dword ptr [$S2]    ; eax 레지스터에 가져옴
		or			ecx, 1                  ; 1로 만듬
		mov			dword ptr [$S2], ecx    ; 저장
		call GetOne                         ; 초기화
		mov dword ptr [s_Val], eax          ; s_Val에 저장

	END:
		mov			esp, ebp
		pop			ebp
		ret
~~~


$S2는 여러개를 사용해야할까?
* 한개를 공유한다. bit 단위로
* 만약 bit가 모자르다면 $S3를 만들어서 사용한다.

다중 스레드 환경에서 안전하지 않다.
* msdn 다중 스레드 프로그램에서 정적 지역 변수에 값을 할당하는 것을 추천하지 않는다.


클래스의 생성자도 초기화 함수에 포함시킬 수 있다.


### 2.3.4 초기화 제어 순서
지금까지 내용을 정리하면 다음과 같은 순서로 초기화가 진행된다.
1. 전역 변수와 정적 변수의 상수 초기화
2. 전역 변수, 정적 전역 변수, 정적 멤버 변수의 함수 초기화
3. 정적 지역 변수의 함수 초기화, 2와 동급

2번과 3번은 어떤 것이 먼저 초기화가 될지 알 수 없다.
* undefined behavior 발생 가능

초기화 순서 제어
* 정적 지역 변수를 사용
* 함수의 흐름을 만들어준다.