# Header File

### 헤더파일이란?

헤더 파일은 바로 이 메뉴판에 비유할 수 있습니다. 헤더 파일에 내가 만든 **함수들을 정리**해 놓음으로써 관리 및 사용하기 쉬워집니다.


>음식점을 예로 들어보겠습니다. <br>하나의 음식점에서는 여러 가지 음식을 파는데요. 
>다양한 음식 관리에 도움을 주는 존재가 있습니다.<br>그것은 바로 메뉴판인데요. 메뉴판이 있으면 주인 입장에서는 내가 만든 메뉴가 어떤게 있는지 한눈에 알아볼 수 있고, 손님 입장에서도 메뉴판을 보고 원하는 음식을 주문할 수 있습니다.

 헤더파일은 크게 두 가지 유형이 있습니다.<br>stdio.h 와 같은 c언어 표준 파이브러리는 꺽쇠 ( <b><i><></i></b> )를 사용해서 불러오고,<br> 유저가 만든 임의의 헤더 파일은 쌍따옴표(<b><i> ““</i></b> ) 로 묶어서 불러옵니다. <br>⚠️이 때 주의해야할 점은 헤더 파일이 메인 코드와 같은 디렉토리 내에 존재할때는 위 코드 처럼 헤더파일 이름만 적어줘도 좋지만, <br>만약 헤더파일이 메인 코드와 다른 디렉토리에 존재한다면 경로를 적어줘야합니다.

<br>

```c
// 예시
#include <stdio.h>
#include "customHeader.h"
```

<br>

### 밑에는 가장 기본적인 형태의 header파일입니다.

```c
// customHeader.h 

#ifndef __CUSTOM_H__
#define __CUSTOM_H__
void print_hello(void);
#endif

```

<br>

여기서 특이한 점은 앞에서 배우지 못했던 전처리인 #ifndef와 #endif가 보입니다.

~~~c

1. 가장 기본적인 분기 

#if 조건 
    코드1

# elif 조건2
    코드2

# else 
    코드3

# endif 


2. 매크로 정의가 되어있는 것을 기준으로 분기

# ifdef 매크로
    코드1
# else
    코드 2
# endif

3. 매크로 정의가 안되어있는 것을 기준으로 분기

# ifndef 매크로
    코드 1
# else 
    코드 2
# endif

~~~

### 위 전처리들이 필요한 이유는 뭘까?

헤더파일을 include 할 때 이중포함 및 컴파일을 방지하기 위해서 입니다. 코드와 함께 보시죠

~~~c
// b.h

struct point {
int x;
int y;
};

~~~

~~~c
// a.h
#include "b.h"

~~~

~~~c
// source.c

#include "a.h"
#include "b.h"
int main(void)
{
    return 0;
}

~~~

위 구조를 앞에서 배운 -E 옵션으로 전처리 작업을 하면 다음과 같은 구조가 된다.

~~~c
// gcc –E source.c

…
struct point { // #include "a.h" 에서 온 코드
int x;
int y;
};


struct point { // #include "a.h" 에서 온 코드
int x;
int y;
};

int main(void)
{
return 0;

~~~

중복으로 코드가 포함된다. 그러므로 위에서 배운 전처리 분기로 해결할 수 있습니다.

