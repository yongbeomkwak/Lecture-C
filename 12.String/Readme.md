# 문자열

C 언어에서는 문자 자료형인 char는 있지만 문자열을 저장하는 자료형은 없습니다.

<br>

## char 포인터 이용한 문자열처리

문자열은 char 포인터 형식으로 사용합니다.

    char *변수이름 = "문자열";

```c
#include <stdio.h>

int main()
{
    char c1 = 'a';         // 변수에 문자 'a' 저장
    char *s1 = "Hello";    // 포인터에 문자열 "Hello"의 주소 저장

    printf("%c\n", c1);    // a: %c로 문자 출력
    printf("%s\n", s1);    // Hello: %s로 문자열 출력

    return 0;
}

```

<br>
<img src ="https://github.com/yongbeomkwak/Lecture-C/assets/48616183/a73f0aeb-32d6-4440-8a0f-89abeea7bc41">

<br>

우리가 글을 쓸 때 문장 끝에 마침표(.)를 찍는 것처럼 C 언어는 문자열 끝에 널 문자를 붙이자고 정했습니다(널 문자 직전까지 문자열로 본다는 뜻). 

즉, 마침표와 같은 역할이죠. 하지만 널 문자는 눈에 보이지 않아서 항상 C 언어 초보자를 괴롭힙니다.

~~~c

# include <stdio.h>

int main() {

    char *s1 = "Hello"; 

    printf("%p\n",s1);  // 0x100123f94
    printf("%p\n",s1+1); // 0x100123f95    +1 

    printf("%c\n",*s1); // H
    printf("%c\n",*(s1+1)); // e
    printf("%c\n",s1[1]); // e 

    printf("%p\n",s1+4); // 0x100123f98 +4 (시작메모리 기준)
    printf("%c\n",*(s1+4)); // o
    printf("%c\n",s1[4]); // o

    printf("%p\n",s1+5); // 0x100123f99 + 5 (시작메모리 기준)
    printf("%d\n", '\0' == *(s1+5)); // 1 : 5번째 요소가 널문자가 참이라는 뜻
    printf("%d\n", '\0' ==  s1[5]); // 1 :  5번째 요소가 널문자가 참이라는 뜻

}

~~~

<br>

## char 배열을 이용한 문자열처리

이전 단계에서 배열도 곧 포인터라고 배웠죠 ?? 그리고 위에서 char 타입 포인터를 이용하여 문자열을 저장했습니다. 그렇다면 배열로도 당연히 가능하겠죠??

    char 배열이름[크기] = "문자열";

~~~c
#include <stdio.h>

int main()
{
       char s1[10] = "Hello";  // 크기가 10인 char형 배열을 선언하고 문자열 할당

    printf("%s\n", s1);     // Hello: %s로 문자열 출력


    printf("%d\n",s1[7] == '\0'); // 1 NULL 문자
    printf("%d\n",s1[9] == '\0'); // 1 NULL 문자 
    printf("%d\n",s1[10] == '\0'); // 0 범위 벗어남

    return 0;  
}
~~~

<img src = "https://github.com/yongbeomkwak/Lecture-C/assets/48616183/21dde61c-5f8e-424c-adbe-ef3944ba668f">

<br>

단, 여기서 배열로 문자열을 사용할 때 한 가지 주의할 점은 배열을 선**언한 즉시 문자열로 초기화**해야 한다는 점입니다. 배열을 미리 선언해놓고 문자열을 나중에 할당할 수는 없습니다.

<br><br>

## 입력받기

### 1. 배열에 입력 받기
~~~c
#include <stdio.h>

int main()
{
    char s1[10];    // 크기가 10인 char형 배열을 선언

    printf("문자열을 입력하세요: ");
    scanf("%s", s1);     // 표준 입력을 받아서 배열 형태의 문자열에 저장

    printf("%s\n", s1);  // 문자열의 내용을 출력

    return 0;
}

~~~

### 2. 포인터에 입력 받기
~~~c
#include <stdio.h>
#include <stdlib.h>    // malloc, free 함수가 선언된 헤더 파일

int main()
{
    char *s1 = malloc(sizeof(char) * 10);    // char 10개 크기만큼 동적 메모리 할당

    printf("문자열을 입력하세요: ");
    scanf("%s", s1);      // 표준 입력을 받아서 메모리가 할당된 문자열 포인터에 저장

    printf("%s\n", s1);   // 문자열의 내용을 출력

    free(s1);    // 동적 메모리 해제

    return 0;
}

~~~

### ⚠️ 주의!

scanf에서 서식 지정자 %s로 문자열을 저장할 때 입력된 문자열에 공백이 있다면 문자열 포인터에는 *_공백 직전_* 까지만 저장됩니다. 

예를 들어 중간에 공백이 있는 Hello, world!를 입력하면 Hello,까지만 저장됩니다

<br>

### [string.h 관련 참고자료](https://modoocode.com/76)