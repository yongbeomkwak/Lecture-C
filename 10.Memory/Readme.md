# Memory

### 1. malloc & free

malloc : memory allocation

    pointer 변수 = malloc(size_t_Size) // 성공하면 메모리 주소를 반환, 실패하면 NULL을 반환
    
~~~c
    

#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    int num1 = 20;    // int형 변수 선언
    int *numPtr1;     // int형 포인터 선언

    numPtr1 = &num1;  // num1의 메모리 주소를 구하여 numPtr에 할당

    int *numPtr2;     // int형 포인터 선언

    numPtr2 = malloc(sizeof(int));    // int의 크기 4바이트만큼 동적 메모리 할당

    printf("%p\n", numPtr1);    // 006BFA60: 변수 num1의 메모리 주소 출력
                                // 컴퓨터마다, 실행할 때마다 달라짐

    printf("%p\n", numPtr2);     // 009659F0: 새로 할당된 메모리의 주소 출력
                                // 컴퓨터마다, 실행할 때마다 달라짐

    free(numPtr2);    // 동적으로 할당한 메모리 해제

    return 0;
}

~~~

<br>

### 2. memset & free

memset: memory set

    memset(포인터, 설정할값, 크기);
    void *memset(void *_Dst, int _Val, size_t _Size);
    값 설정이 끝난 포인터를 반환


~~~c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일
#include <string.h>    // memset 함수가 선언된 헤더 파일

int main()
{
    long long *numPtr = malloc(sizeof(long long));  // long long의 크기 8바이트만큼 동적 메모리 할당

    memset(numPtr, 0x27, 8);    // numPtr이 가리키는 메모리를 8바이트만큼 0x27로 설정

    printf("0x%llx\n", *numPtr);    // 0x2727272727272727: 27이 8개 들어가 있음

    free(numPtr);    // 동적으로 할당한 메모리 해제

    return 0;
}
~~~

<br>

### NULL 포인터

NULL이 들어있는 포인터를 널 포인터(null pointer)라고 하며 아무것도 가리키지 않는 상태를 뜻합니다.

~~~c
#include <stdio.h>

int main()
{
    int *numPtr1 = NULL;    // 포인터에 NULL 저장

    printf("%p\n", numPtr1);    // 00000000

    return 0;
}
~~~