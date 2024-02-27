## 변수

- 기본형식

    ```c
    타입 변수명 = 값;

    타입 변수명1 = 값

    타입 변수명2= 값2, 변수명3 = 값3


    int main()
    {
        int num1 = 10;               // 변수를 선언하면서 값 할당(초기화)
        int num2 = 20, num3 = 30;    // 변수 여러 개를 선언하면서 값 할당(초기화)

        printf("%d %d %d\n", num1, num2, num3);    // 10 20 30: 변수에 저장된 값을 %d로 출력

        return 0;
    }


    ```

- 정의와 초기화 따로

    ```c
    
    타입 변수명1, 변수명2, 변수명3;

    변수명1 = 값1
    변수명2 = 값2 
    ...

    #include <stdio.h>

    int main()
    {
        int num1 = 10;               // 변수를 선언하면서 값 할당(초기화)
        int num2 = 20, num3 = 30;    // 변수 여러 개를 선언하면서 값 할당(초기화)

        printf("%d %d %d\n", num1, num2, num3);    // 10 20 30: 변수에 저장된 값을 %d로 출력

        return 0;
    }



    ```

    ## 출력문 포맷

- `%d` : int값을 부호있는 10진수로 출력

- `%i` : d와 같음

- `u` : int값을 부호없는 10진수로 출력
- `X` : int값을 부호없는 16진수로 출력  10~15은  'A'~'F'로 표시
- `x` : int값을 부호없는 16진수로 출력  10~15은  'a'~'f'로 표시
- `o` : int값을 부호없는 8진수로 출력
- `p` : 포인터값을 16진수로 출력
- `s` : 문자열 출력
- `c` : int값을 문자로 출력
- `C`:  c와 같음
- `f` : double값을 소수로 출력 (예：12.566371)
- `e` : double값을 지수로 출력 (예：1.256637e+001)
- `E` : e와 같음 'e'가 'E'로 표시 (예：1.256637E+001)。
- `g` : 숫자값의 크기에 따라 f나 e로 출력  (예：12.5664、2.99792e+008) 숫자값의 절대치가 너무 커서 precision의 자리수를 넘는 경우와 숫자값의 절대값이 0.0001보다 작은 경우 e형식이 사용되어짐. 그 외의 경우는 f형식으로 사용됨
- `G` : 9와 같음 'e'가 'E'로 표시

```c

#include <stdio.h>
void main()

{


    int        nData1 = 337;

    int        nData2 = -777;

    double    dData = 3.141259;

    double    dData2 = 314125912345;

    double    dData3 = 0.00002;

    char    cData = 'X';

    char    szData[5] = "ABC";


    printf("부호있는 10진수 정수:%%d %d\n", nData1);

    printf("부호있는 10진수 정수:%%d %d\n", nData2);

    printf("부호없는 10진수 정수:%%u %u\n", nData1);

    printf("부호없는 16진수 정수:%%x %x\n", nData1);

    printf("부호없는 16진수 정수:%%X %X\n", nData1);

    printf("부호없는 08진수 정수:%%o %o\n", nData1);

    printf("    16진수 포인터값:%%p %p\n", szData);

    printf("        문자열 출력:%%s %s\n", szData);

    printf("           문자 출력:%%c %c\n", cData);

    printf("           문자 출력:%%C %C\n", cData);

    printf("  double값 소수 출력:%%f %f\n", dData);

    printf("  double값 지수 출력:%%e %e\n", dData);

    printf("  double값 지수 출력:%%E %E\n", dData);

    printf("  값에 따른 f/e 출력:%%g %g\n", dData);

    printf("  값에 따른 f/e 출력:%%g %g\n", dData2);

    printf("  값에 따른 f/e 출력:%%G %G\n", dData2);

    printf("  값에 따른 f/e 출력:%%G %G\n", dData3);

}


```