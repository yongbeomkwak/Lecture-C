# 구조체

### 기본 선언

~~~c
struct 구조체이름 {
    자료형 멤버이름;
};
~~~

### typedef를 사용하여 별칭 부여

~~~c
typedef struct 구조체이름(태그) {
    자료형 멤버이름;
} 구조체별칭 , *P구조체포인터 별칭;
~~~

### 구조체 멤버 할당 및 접근 

~~~c

// 정의 

1. struct 구조체이름 변수이름;

2. 구조체별칭 변수이름;

3. struct 구조체이름 *포인터이름 = malloc(sizeof(struct 구조체이름));

4. 구조체별칭 *포인터이름 = malloc(sizeof(구조체별칭));

// 멤버 접근 

구조체 변수.해당 멤버변수

구조체 포인터변수->해당 변수

~~~

### 구조체 크기

~~~c
sizeof(struct 구조체)
sizeof(구조체별칭)
sizeof(구조체변수)


#include <stdio.h>

struct PacketHeader {
    char flags;    // 1바이트
    int seq;       // 4바이트
};

int main()
{
    struct PacketHeader header;

    printf("%d\n", sizeof(header.flags));           // 1: char는 1바이트
    printf("%d\n", sizeof(header.seq));             // 4: int는 4바이트
    printf("%d\n", sizeof(header));                 // 8: 구조체 전체 크기는 8바이트
    printf("%d\n", sizeof(struct PacketHeader));    // 8: 구조체 이름으로 크기 구하기

    return 0;
}

PacketHeader 구조체 안에는 1바이트 크기의 char와 4바이트 크기의 int가 들어있습니다. 그래서 전체 크기는 5바이트가 나와야 할 것 같은데 실제로는 8바이트가 나왔습니다.

C 언어에서는 구조체를 정렬할 때 멤버 중에서 가장 큰 자료형 크기의 배수로 정렬합니다. 여기서 가장 큰 자료형은 int이므로 int의 크기 4바이트를 기준으로 정렬합니다.


데이터 전송이나 저장을 할 때 구조체 정렬을 피하려면 어떻게 해야 할까요?


Visual Studio, GCC 4.0 이상
#pragma pack(push, 정렬크기)
#pragma pack(pop)

GCC 4.0 미만
__attribute__((aligned(정렬크기), packed))


#include <stdio.h>

#pragma pack(push, 1)    // 1바이트 크기로 정렬
struct PacketHeader {
    char flags;    // 1바이트
    int seq;       // 4바이트
};
#pragma pack(pop)        // 정렬 설정을 이전 상태(기본값)로 되돌림

int main()
{
    struct PacketHeader header;

    printf("%d\n", sizeof(header.flags));    // 1: char는 1바이트
    printf("%d\n", sizeof(header.seq));      // 4: int는 4바이트
    printf("%d\n", sizeof(header));          // 5: 1바이트 단위로 정렬했으므로 

 // 구조체 전체 크기는 5바이트

    return 0;
}

// ------------------------------------------------------------------------

#pragma pack(push, 1)을 한 번 사용하면 그 아래에 오는 모든 구조체에 영향을 주므로 정렬 설정을 한 뒤에는 
#pragma pack(pop)를 사용하여 설정을 이전 상태로 되돌립니다.


GCC 4.0 미만은 __attribute__((aligned(정렬크기), packed)) 이용

#include <stdio.h>

struct PacketHeader {
    char flags;    // 1바이트
    int seq;    // 4바이트
} __attribute__((aligned(1), packed));    // GCC 4.0 미만: 1바이트 크기로 정렬

int main()
{
    struct PacketHeader header;

    printf("%d\n", sizeof(header.flags));     // 1: char는 1바이트
    printf("%d\n", sizeof(header.seq));       // 4: int는 4바이트
    printf("%d\n", sizeof(header));           // 5: 1바이트 단위로 정렬했으므로 
    // 구조체 전체 크기는 5바이트

    return 0;
}


~~~

### 구조체와 메모리 복사하기

    memcpy(목적지포인터, 원본포인터, 크기);

~~~c
#include <stdio.h>
#include <string.h>    // memcpy 함수가 선언된 헤더 파일

struct Point2D {
    int x;
    int y;
};

int main()
{
    struct Point2D p1;
    struct Point2D p2;

    p1.x = 10;    // p1의 멤버에만 값 저장
    p1.y = 20;    // p1의 멤버에만 값 저장

    memcpy(&p2, &p1, sizeof(struct Point2D));    // Point2D 구조체 크기만큼 p1의 내용을 p2로 복사

    printf("%d %d\n", p2.x, p2.y);    // 10 20: p1의 내용을 p2로 복사했으므로 10 20

    return 0;
}

#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일
#include <string.h>    // memcpy 함수가 선언된 헤더 파일

struct Point2D {
    int x;
    int y;
};


malloc을 사용할 때는

int main()
{
    struct Point2D *p1 = malloc(sizeof(struct Point2D));
    struct Point2D *p2 = malloc(sizeof(struct Point2D));

    p1->x = 10;    // p1의 멤버에만 값 저장
    p1->y = 20;    // p1의 멤버에만 값 저장

    memcpy(p2, p1, sizeof(struct Point2D));    // Point2D 구조체 크기만큼 p1의 내용을 p2로 복사

    printf("%d %d\n", p2->x, p2->y);    // 10 20: p1의 내용을 p2로 복사했으므로 10 20

    free(p2);
    free(p1);

    return 0;
}

~~~

### 구조체 배열 선언

    struct 구조체이름 변수이름[크기] = { { .멤버이름1 = 값1, .멤버이름2 = 값2 }, { .멤버이름1 = 값3, .멤버이름2 = 값4 } };
    
    struct 구조체이름 변수이름[크기] = { { 값1, 값2 }, { 값3, 값4 } };

~~~c
#include <stdio.h>

struct Point2D {
    int x;
    int y;
};

int main()
{
    // 구조체 배열을 선언하면서 초기화
    struct Point2D p1[3] = { { .x = 10, .y = 20 }, { .x = 30, .y = 40 }, { .x = 50, .y = 60 } };

    printf("%d %d\n", p1[0].x, p1[0].y);    // 10 20
    printf("%d %d\n", p1[1].x, p1[1].y);    // 30 40
    printf("%d %d\n", p1[2].x, p1[2].y);    // 50 60

    // 구조체 배열을 선언하면서 초기화
    struct Point2D p2[3] = { { 10, 20 }, { 30, 40 }, { 50, 60 } };

    printf("%d %d\n", p2[0].x, p2[0].y);    // 10 20
    printf("%d %d\n", p2[1].x, p2[1].y);    // 30 40
    printf("%d %d\n", p2[2].x, p2[2].y);    // 50 60

    return 0;
}

~~~

    struct 구조체이름 *포인터이름[크기];

~~~c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

struct Point2D {
    int x;
    int y;
};

int main()
{
    struct Point2D *p[3];    // 크기가 3인 구조체 포인터 배열 선언

    // 구조체 포인터 배열 전체 크기에서 요소(구조체 포인터)의 크기로 나눠서 요소 개수를 구함
    for (int i = 0; i < sizeof(p) / sizeof(struct Point2D *); i++)    // 요소 개수만큼 반복
    {
        p[i] = malloc(sizeof(struct Point2D));    // 각 요소에 구조체 크기만큼 메모리 할당
    }

    p[0]->x = 10;    // 인덱스로 요소에 접근한 뒤 화살표 연산자로 멤버에 접근
    p[0]->y = 20;
    p[1]->x = 30;
    p[1]->y = 40;
    p[2]->x = 50;
    p[2]->y = 60;

    printf("%d %d\n", p[0]->x, p[0]->y);    // 10 20
    printf("%d %d\n", p[1]->x, p[1]->y);    // 30 40
    printf("%d %d\n", p[2]->x, p[2]->y);    // 50 60

    for (int i = 0; i < sizeof(p) / sizeof(struct Point2D *); i++)    // 요소 개수만큼 반복
    {
        free(p[i]);    // 각 요소의 동적 메모리 해제
    }

    return 0;
}

~~~