# 반복문 

## for 문

    for (초기식; 조건식; 변화식) // ← 루프 선언문(loop statement)
    {
        반복할 코드
    }
    // ↑ 루프 본체(loop body)

```c
// 기본

for (int i = 0; i < 100; i++)
{  
    printf("for 반복문\n");
}


// 변수 2개 이용


for (int i = 0, j = 0; i< 10 && j<5 ; i++, j+=2)
{
    printf("i: %d, j: %d\n", i, j);
}

/*
    i: 0, j: 0
    i: 1, j: 2
    i: 2, j: 4
*/


```

## while

    while (조건식) {
        반복할 코드
    }

```c

#include <stdio.h>

int main() {


    int a = 0;

    while (a < 10) {

        printf("%d\n",a);

        a++;
    }

}

```

## do-while

    do { 
        반복할 코드 (조건에 상관없이 무조건 최초 실행은 됨)
    } while(조건식);

```c

int main() {


    int a = 10;
    
    do
    {
        printf("%d\n", a);

        a++;

    } while (a<10);

    printf("%d\n", a);

}
// 결과
// 10
// 11

```

## 제어문

### 1. continue
- continue 밑의 코드를 실행하지 않고 다음 반복으로 진행

### 2. break
- break 밑의 코드를 실행하지 않고 반복문 탈출