# 조건문

<br>

## if, else if, else

```c

if 조건1
{
    코드1
}
else if 조건2
{
    코드2
}
else if 조건3
{
    코드3
}
else
{
    모두 포함되지 않은 때 실행될 코드
}


```

## switch case

```c

// 간단한 코드 실행 
switch (판단할 변수)
{
    case 조건1:
        코드 1
        break;
    
    case 조건2:
        코드 2
        break;
    
    .
    .
    .

    default:
        아무 case에도 해당되지 않았을 때 실행한 코드

}

// case안에서 변수를 할당하려면 중괄호를 이용해야함

switch (num1)    // num1의 값에 따라 분기
{
case 1:
{   // case에서 변수를 선언하려면 중괄호로 묶어줌
    int num2 = num1;
    printf("%d입니다.\n", num2);
    break;
}
case 2:
    printf("2입니다.\n");
    break;
default:
    printf("default\n");
    break;
}



```