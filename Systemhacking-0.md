# System hacking-0

---



| Author       | Mingwan Jeong (chongchong/jeongmingwan3@gmail.com) |
| ------------ | ---------------------------------------- |
| Date created | 2022.12.07                               |



## Index

1. Pwnable 유래 
2. 버그 에러차이점 
3. 취약점의 정의
4. 취약점 버그관계
5. 취약한 코드 구성(gets)
6. 카나리유래
7. Gdb 명령어 

---

시스템해킹과 웹해킹 단하나의 목표 = 니꺼내꺼 내꺼내꺼 , 그런데 상식적으로 쉬울까? 

Linux pwnable = system hacking

### 1. Pwnable 유래

pwnable -> (기원) own + able p는 오타다. 학계의 정설

관리자 권한을 탈취해 자기것으로 만든다.



### 2. 버그와 에러의 차이점

버그는 프로그래머가 의도하지 않은 모든 동작들이 버그다.

에러는 오류, 잘못된 것 , 사용자 이슈다.

​

### 3. 취약점의 정의

취약점은 공격자가 주어진 권한 이상의 권한을 획득하거나 프로그래머가 의도하지 않은 동작을 수행할 수 있도록 하는 소프트웨어 버그다.

### 4. 취약점과 버그의 관계

![스크린샷 2022-12-08 15.43.15](/Users/jmg/Desktop/스크린샷 2022-12-08 15.43.15.png)

취약점 ⊂ 버그

안정적으로 공격할수있는 취약점 ⊂ 안정적이지 않은 취약점⊂ 알파 분류법상으로 있음 ⊂버그



### 5. 취약한 코드 구성(gets)

​

```c
#include <stdio.h>
int main() {
	Char buf[5];
	gets(buf);
	return 0;
}
```



### 6. 카나리 유래

카나리가 사람보다 유독가스에 취약해 먼저 죽었기 때문에 광산에 유독가스 탐지를 위해 데려간 것에서 유래한다.

카나리 보호기법은 buffer와 SFP(Stack Frame Pointer) 사이에 buffer overflow를 탐지하기 위한 임의의 데이터를 삽입하는 기법이다.

버퍼 오버플로가 발생하면 Canary 값이 손상되며 Canaries 데이터의 검증에 실패하여 오버플로에 대한 경고가 출력되고 손상된 데이터를 무효화 처리한다.

![스크린샷 2022-12-08 17.26.01](/Users/jmg/Desktop/스크린샷 2022-12-08 17.26.01.png)  



### 6. Gdb 명령어(checksec, r)

Gnu c debugger =gdb

다른 프로그램 수행 중에 그 프로그램 ‘내부에서’ 무슨 일이 일어나고 있는지 보여주거나 프로그램이 잘못 실행되었을 때 무슨 일이 일어나고 있는지 보여준다.

Ex) stack smashing detected terminated > 를 gdb로 자세하게 볼수있다.

- 명령어 

  -checksec = check security : 현재 바이너리에 걸려있는 mitigation 정보들을 보여준다.

  -r = run : 프로그램을 실행시켜 이상이 발생했을때의 파일과 지점을 출력해준다. 오류 지점에 도달하기 전 과정을 확인하기 위해서는 다음 명령어를 이용하면 된다.
