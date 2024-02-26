## 1. 정수형


### 특징
정수 자료형은 크게 char, int가 있으며 앞에 부호 키워드(signed, unsigned)와 크기(short, long)를 붙여서 특성을 정의할 수 있습니다.

- signed: 부호 있는 정수를 표현합니다. 보통 signed 키워드는 생략합니다.

- unsigned: 부호 없는 정수를 표현합니다. 따라서 값은 0부터 시작하게 됩니다.

<img src = "https://github.com/yongbeomkwak/Lecture-C/assets/48616183/01440604-deb6-4bb9-a8a8-359face63767">


### 오버 플러우

저장할 수 있는 범위를 넘어서면 최솟값부터 다시 시작하게 됩니다. 

반대로 최솟값보다 작아지면 언더플로우(underflow)가 발생하여 최댓값부터 다시 시작하게 됩니다(값을 계속 뺀다면 최댓값에서 값이 계속 작아짐)

<img src = "https://github.com/yongbeomkwak/Lecture-C/assets/48616183/157eb584-763c-4cc9-9668-14cdf26760eb">

~~~c 
// 사이즈 크기 구하기

sizeof 표현식
sizeof(자료형)
sizeof(표현식)
// 바이트르 뱉어냄


int main()
{

    int num1 = 0;
    int size;

    size = sizeof num1;    // 변수 num1의 자료형 크기를 구함

    printf("num1의 크기: %d\n", size);
    
    printf("char: %d, short: %d, int: %d, long: %d, long long: %d\n",
        sizeof(char),        // 1: sizeof로 char 자료형의 크기를 구함
        sizeof(short),       // 2: sizeof로 short 자료형의 크기를 구함
        sizeof(int),         // 4: sizeof로 int 자료형의 크기를 구함
        sizeof(long),        // 4: sizeof로 long 자료형의 크기를 구함
        sizeof(long long)    // 8: sizeof로 long long 자료형의 크기를 구함
    );

    return 0;
}

~~~

### 다양한 기본 헤더 파일

~~~c 
// 최솟값과 최댓값 표현하기
#include <stdio.h>
#include <limits.h>    // 자료형의 최댓값과 최솟값이 정의된 헤더 파일

int main()
{
    char num1 = CHAR_MIN;          // char의 최솟값
    short num2 = SHRT_MIN;         // short의 최솟값
    int num3 = INT_MIN;            // int의 최솟값
    long num4 = LONG_MIN;          // long의 최솟값
    long long num5 = LLONG_MIN;    // long long의 최솟값

    // char, short, int는 %d로 출력하고 long은 %ld로 출력, long long은 %lld로 출력
    printf("%d %d %d %ld %lld\n", num1, num2, num3, num4, num5);
    // -128 -32768 -2147483648 -2147483648 -9223372036854775808

    return 0;
}
~~~

<br>

~~~c
#include <stdio.h>
#include <stdint.h>    // 크기별로 정수 자료형이 정의된 헤더 파일

int main()
{
    int8_t num1 = -128;                    // 8비트(1바이트) 크기의 부호 있는 정수형 변수 선언
    int16_t num2 = 32767;                  // 16비트(2바이트) 크기의 부호 있는 정수형 변수 선언 
    int32_t num3 = 2147483647;             // 32비트(4바이트) 크기의 부호 있는 정수형 변수 선언
    int64_t num4 = 9223372036854775807;    // 64비트(8바이트) 크기의 부호 있는 정수형 변수 선언

    // int8_t, int16_t, int32_t는 %d로 출력하고 int64_t는 %lld로 출력
    printf("%d %d %d %lld\n", num1, num2, num3, num4); // -128 32767 2147483647 9223372036854775807

    uint8_t num5 = 255;                      // 8비트(1바이트) 크기의 부호 없는 정수형 변수 선언
    uint16_t num6 = 65535;                   // 16비트(2바이트) 크기의 부호 없는 정수형 변수 선언
    uint32_t num7 = 4294967295;              // 32비트(4바이트) 크기의 부호 없는 정수형 변수 선언
    uint64_t num8 = 18446744073709551615;    // 64비트(8바이트) 크기의 부호 없는 정수형 변수 선언

    // uint8_t, uint16_t, uint32_t는 %u로 출력하고 uint64_t는 %llu로 출력
    printf("%u %u %u %llu\n", num5, num6, num7, num8); // 255 65535 4294967295 18446744073709551615

    return 0;
}

~~~

<br><br><br>

## 2. 실수자료형

### 특징

소수점을 표현할 수 있는 실수를 변수에 저장해보겠습니다.

다음은 실수 자료형의 크기와 저장할 수 있는 값의 범위입니다

(여기 나오는 모든 내용을 외울 필요는 없습니다. 실수 자료형의 크기 정도만 기억하면 되고, 나머지는 나중에 필요할 때 찾아보세요).

<br>

<img src ="https://github.com/yongbeomkwak/Lecture-C/assets/48616183/671b9e41-13a0-4507-904b-338128fc56c6">

<br><br>

컴퓨터에서는 값을 0과 1로 저장합니다. 그래서 실수도 0과 1로 저장해야 하는데 이렇게 실수와 소수점을 2진수로 표현하는 방식을 부동소수점 표현 방식이라고 합니다. 

부동소수점 방식은 자료형의 일정 부분을 비트 단위로 나누어 부호, 가수(significand), 기수(base), 지수(exponent)를 저장하여 실수를 표현합니다.

부동소수점은 다음과 같이 기수(n)를 지수(p)만큼 거듭제곱한 값을 가수(m)와 곱하는 방식을 사용합니다. 단, 컴퓨터는 값을 저장할 때 2진수로 저장하므로 기수(밑수)는 2로 고정되어 있으며 2 자체는 따로 저장하지 않습니다.


**부동소수점**
$$\pm m \times n^p$$

<br>
p가 양수면 정수, p가 음수면 소수

<br>

<table align ="center">

  <thead>
    <tr>
      <th scope="col">자료형</th>
      <th scope="col">크기</th>
      <th scope="col">부호</th>
      <th scope="col">지수</th>
      <th scope="col">가수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">float</th>
      <td>32bit</td>
      <td>1bit</td>
      <td>8bit</td>
      <td>23bit</td>
    </tr>
    <tr>
      <th scope="row">double</th>
      <td>64bit</td>
      <td>1bit</td>
      <td>11bit</td>
      <td>52bit</td>
    </tr>
    
  </tbody>
</table>

<br>

~~~c
// 저장과 출력

#include <stdio.h>

int main()
{
    float num1 = 0.1f;               // 단정밀도 부동소수점 변수를 선언하고 값을 할당
                                     // float는 숫자 뒤에 f를 붙임

    double num2 = 3867.215820;       // 배정밀도 부동소수점 변수를 선언하고 값을 할당
                                     // double은 숫자 뒤에 아무것도 붙이지 않음

    long double num3 = 9.327513l;    // 배정밀도 부동소수점 변수를 선언하고 값을 할당
                                     // long double은 숫자 뒤에 l을 붙임

    // float와 double은 %f로 출력, long double은 %Lf로 출력
    printf("%f %f %Lf\n", num1, num2, num3);    // 0.100000 3867.215820 9.327513

    return 0;
}

~~~

<br>

~~~c
// 지수 표기법

#include <stdio.h>

int main()
{
    float num1 = 3.e5f;             // 지수 표기법으로 300000을 표기
                                    // float는 숫자 뒤에 f를 붙임
 
    double num2 = -1.3827e-2;       // 지수 표기법으로 -0.013827을 표기
                                    // double은 숫자 뒤에 아무것도 붙이지 않음

    long double num3 = 5.21e+9l;    // 지수 표기법으로 5210000000을 표기
                                    // long double은 숫자 뒤에 l을 붙임

    // float와 double은 %f로 출력, long double은 %Lf로 출력
    printf("%f %f %Lf\n", num1, num2, num3); // 300000.000000 -0.013827 5210000000.000000

    // 지수 표기법으로 출력할 때는 float와 double은 %e로 출력, long double은 %Le로 출력
    printf("%e %e %Le\n", num1, num2, num3); // 3.000000e+05 -1.382700e-02 5.210000e+09

    return 0;
}

~~~

<br>

### 다양한 헤더 기본 파일

~~~c
// 최댓값 쵯소값

#include <stdio.h>
#include <float.h>    // 실수 자료형의 양수 최솟값, 최댓값이 정의된 헤더 파일

int main()
{
    float num1 = FLT_MIN;           // float의 양수 최솟값
    float num2 = FLT_MAX;           // float의 양수 최댓값
    double num3 = DBL_MIN;          // double의 양수 최솟값
    double num4 = DBL_MAX;          // double의 양수 최댓값
    long double num5 = LDBL_MIN;    // long double의 양수 최솟값
    long double num6 = LDBL_MAX;    // long double의 양수 최댓값

    printf("%.40f %.2f\n", num1, num2);    // 0.0000000000000000000000000000000000000118
                                           // 340282346638528859811704183484516925440.00

    printf("%e %e\n", num3, num4);         // 2.225074e-308 1.797693e+308
    printf("%Le %Le\n", num5, num6);       // 2.225074e-308 1.797693e+308
 
    return 0;
}

~~~

<br><br><br>

## 문자 자료형

### 특징

- C 언어에서는 정수 자료형인 char를 이용하여 문자 한 개를 저장합니다. 다음은 문자 자료형의 크기와 저장할 수 있는 범위입니다.

<br>

<img src = "https://github.com/yongbeomkwak/Lecture-C/assets/48616183/f92a458e-7ff8-4ce7-8b28-69d97bc4c907">

<br>

char에 문자를 저장할 때는 문자 자체를 저장하는 것이 아니라 문자에 해당하는 정숫값을 저장하게 됩니다.

```c

int main()
{

    // C 언어에서 문자는 ' ' (작은따옴표)로 묶어서 표현합니다.

    char c1 = 'a';    // 문자 변수를 선언하고 문자 a를 저장
    char c2 = 'b';    // 문자 변수를 선언하고 문자 b를 저장
 
    // char를 %c로 출력하면 문자가 출력되고, %d로 출력하면 정숫값이 출력됨
    printf("%c, %d\n", c1, c1);    // a, 97: a의 ASCII 코드값은 97
    printf("%c, %d\n", c2, c2);    // b, 98: b의 ASCII 코드값은 98


    printf("%c %d\n", 'a' + 1, 'a' + 1);    // b 98: a는 ASCII 코드값 97이고, 
                                            // 97에 1을 더하여 98이 되었으므로 b가 출력됨

    printf("%c %d\n", 97 + 1, 97 + 1);      // b 98: ASCII 코드값 97에 1을 더하여 98이 되었으므로 
                                            // b가 출력됨
 
    return 0;
}
```

<br><br><br>

## 불 자료형 

### 특징

- 참과 거짓을 나타내는 자료형, 크기가 1이므로 굉장히 효율적


~~~c

#include <stdio.h>
#include <stdbool.h>    // bool, true, false가 정의된 헤더 파일
 
int main()
{
    printf("%d\n", true && true);      // 1: true AND true는 1
    printf("%d\n", true && false);     // 0: true AND false는 0
    printf("%d\n", false && true);     // 0: false AND true는 0
    printf("%d\n", false && false);    // 0: false AND false는 0
 
    printf("%d\n", true || true);      // 1: true OR true는 1
    printf("%d\n", true || false);     // 1: true OR false는 1
    printf("%d\n", false || true);     // 1: false OR true는 1
    printf("%d\n", false || false);    // 0: false OR false는 0

    return 0;
}

~~~