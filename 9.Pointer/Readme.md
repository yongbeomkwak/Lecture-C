# 포인터

메모리 주소는 어디에 저장해야 할까요? C 언어에서 메모리 주소는 포인터(pointer) 변수에 저장합니다.

## 문법
    자료형 *포인터이름; // 선언
    포인터 = &변수; // 할당

    *포인터 변수 // 역참조


```c

int main()
{
    int *numPtr;      // 포인터 변수 선언
    int num1 = 10;    // 정수형 변수를 선언하고 10 저장

    numPtr = &num1;   // num1의 메모리 주소를 포인터 변수에 저장

    printf("%d\n", *numPtr);    // 10: 역참조 연산자로 num1의 메모리 주소에 접근하여 값을 가져옴

    return 0;
}


```


### 역참조를 이용한 값 할당

```c
#include <stdio.h>

int main()
{
    int *numPtr;      // 포인터 변수 선언
    int num1 = 10;    // 정수형 변수를 선언하고 10 저장

    numPtr = &num1;   // num1의 메모리 주소를 포인터 변수에 저장

    *numPtr = 20;     // 역참조 연산자로 메모리 주소에 접근하여 20을 저장

    printf("%d\n", *numPtr);    // 20: 역참조 연산자로 메모리 주소에 접근하여 값을 가져옴
    printf("%d\n", num1);       // 20: 실제 num1의 값도 바뀜

    return 0;
}
```

### 상수와 포인터

포인터에도 const 키워드를 붙일 수 있는데 const 의 위치에 따라 특성이 달라집니다. 

먼저 상수를 가리키는 포인터(pointer to constant)입니다.

~~~c
const int num1 = 10;    // int형 상수
const int *numPtr;      // int형 상수를 가리키는 포인터. int const *numPtr도 같음

numPtr = &num1;
*numPtr = 20;    // 컴파일 에러. num1이 상수이므로 역참조로 값을 변경할 수 없음
~~~

즉, pointer to constant는 메모리 주소에 저장된 값을 변경할 수 없다는 뜻입니다.

<br>

이번에는 포인터 자체가 상수인 상황입니다(constant pointer). 이때는 * 뒤에 const를 붙입니다.

~~~c
int num1 = 10;    // int형 변수
int num2 = 20;    // int형 변수
int * const numPtr = &num1;    // int형 포인터 상수

numPtr = &num2;    // 컴파일 에러. 포인터(메모리 주소)를 변경할 수 없음
~~~

<br>

#### 상수 최종정리

~~~c
const int num1 = 10;    // int형 상수
const int num2 = 20;    // int형 상수
const int * const numPtr = &num1;    // int형 상수를 가리키는 포인터 상수
                                     // int const * const numPtr도 같음

*numPtr = 30;      // 컴파일 에러. num1이 상수이므로 역참조로 값을 변경할 수 없음
numPtr = &num2;    // 컴파일 에러. 포인터(메모리 주소)를 변경할 수 없음
~~~

<br>

### Void 포인터

    void *포인터이름;

<br>

기본적으로 C 언어는 자료형이 다른 포인터끼리 메모리 주소를 저장하면 컴파일 경고(warning)가 발생합니다. 

하지만 void 포인터는 자료형이 정해지지 않은 특성 때문에 어떤 자료형으로 된 포인터든 모두 저장할 수 있습니다. 

반대로 다양한 자료형으로 된 포인터에도 void 포인터를 저장할 수도 있습니다. 이런 특성 때문에 void 포인터는 **범용 포인터**라고 합니다.

~~~c

#include <stdio.h>

int main()
{
    int num1 = 10;
    char c1 = 'a';
    int *numPtr1 = &num1;
    char *cPtr1 = &c1;

    void *ptr;        // void 포인터 선언

    // 포인터 자료형이 달라도 컴파일 경고가 발생하지 않음
    ptr = numPtr1;    // void 포인터에 int 포인터 저장
    ptr = cPtr1;      // void 포인터에 char 포인터 저장

    // 포인터 자료형이 달라도 컴파일 경고가 발생하지 않음
    numPtr1 = ptr;    // int 포인터에 void 포인터 저장
    cPtr1 = ptr;      // char 포인터에 void 포인터 저장

    printf("%d", *ptr);   // void 포인터는 역참조할 수 없음. 컴파일 에러

    
    return 0;
}

~~~

단, void 포인터는 자료형이 정해지지 않았으므로 값을 가져오거나 저장할 크기도 정해지지 않았습니다. 따라서 void 포인터는 역참조를 할 수 없습니다.

그런데 역참조도 할 수 없는 void 포인터는 왜 사용할까요? void 포인터는 되는 게 별로 없어 보이지만 실제로 C 언어에서 다양한 형태로 사용되고 있습니다. 

예를 들자면 함수에서 다양한 자료형을 받아들일 때, 함수의 반환 포인터를 다양한 자료형으로 된 포인터에 저장할 때, 자료형을 숨기고 싶을 때 사용합니다.

<br>

### 이중포인터

금까지 변수의 포인터를 선언했습니다. 그렇다면 포인터의 포인터도 가능하지 않을까요? 이번에는 포인터의 메모리 주소를 저장하는 포인터의 포인터를 선언해보겠습니다.

포인터를 선언할 때 *를 두 번 사용하면 포인터의 포인터(이중 포인터)를 선언합니다.

~~~c
#include <stdio.h>

int main() {

    int *numPtr1; // 단일 포인터 선언
    int **numPtr2;  // 이중 포인터 선언
    int num1 = 10;

    numPtr1 = &num1; // num1의 메모리 주소 저장 
    numPtr2 = &numPtr1;  // numPtr1의 메모리 주소 저장
    
    printf("%p\n",&num1); // num1 변수의 주소
    printf("====== numPtr1 ========\n");
    printf("%p\n",numPtr1); // numPtr1이 저장하고 (가르키는) 주소 == &num1
    printf("%p\n",*numPtr1); // numPtr1 주소의 역참조 == num 값 == 10
    printf("%p\n",&numPtr1); // numPtr1 변수의 주소
    printf("====== numPtr2 ========\n");
    printf("%p\n",numPtr2); // numPtr2이 저장하고 (가르키는) 주소 == &numPtr1 
    printf("%p\n",*numPtr2); // numPtr2의 역참조, numPtr2 -> numPtr1 의 값 &num
    printf("%d\n", **numPtr2); // numPtr2 -> numPtr1 -> num 의 값 10 
    printf("%p\n",&numPtr2); // numPtr2 변수의 주소
}
~~~

## 참고자료

<img src ="https://github.com/yongbeomkwak/Lecture-C/assets/48616183/9f101af3-db3f-440c-9a0f-24ed3f364b6e">