# 입력 

```c 

#define _CRT_SECURE_NO_WARNINGS    // scanf 보안 경고로 인한 컴파일 에러 방지
#include <stdio.h>

int main()
{
    int num1, num2;

    printf("정수를 두 개 입력하세요: ");
    scanf("%d %d", &num1, &num2);    // 값을 두 개 입력받아서 변수 두 개에 저장

    printf("%d %d\n", num1, num2);    // 변수의 내용을 출력

    float num1;

    printf("실수를 입력하세요: ");
    scanf("%f", &num1);    // 실수를 입력받아서 변수에 저장

    char c1;

    printf("문자를 입력하세요: ");
    scanf("%c", &c1);    // 문자를 입력받아서 변수에 저장

    return 0;
}

```