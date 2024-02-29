# 열거형

열거형은 같은 성격을 가진 그룹이라고 생각하시면됩니다.

열거형 이름이나 값을 정의할 때 대문자만 사용하는 경우가 많습니다. 

### 기본
~~~c
enum 열거형이름 {
    값1 = 초깃값,
    값2,
    값3
};
~~~

### typedef를 사용하여 별칭 사용하기

~~~c
typedef enum 열거형이름 {
    값1 = 초깃값,
    값2,
    값3
} 열거형별칭;
~~~

~~~c



typedef enum _DayOfWeek {    // 열거형 이름은 _DayOfWeek
    Sunday = 0,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
} DayOfWeek;                 // typedef를 사용하여 열거형 별칭을 DayOfWeek로 
~~~

### switch문과 같이 사용하기

~~~c
#include <stdio.h>

enum LuxSkill {
    LightBinding = 1,
    PrismaticBarrier,
    LucentSingularity,
    FinalSpark
};

int main()
{
    enum LuxSkill skill;    // 열거형 변수 선언

    skill = LightBinding;    // 열거형 값 할당

    switch (skill)
    {
    case LightBinding:         // 열거형 값이 LightBinding일 때
        printf("LightBinding\n");
        break;
    case PrismaticBarrier:     // 열거형 값이 PrismaticBarrier일 때
        printf("PrismaticBarrier\n");
        break;
    case LucentSingularity:    // 열거형 값이 LucentSingularity일 때
        printf("LucentSingularity\n");
        break;
    case FinalSpark:           // 열거형 값이 FinalSpark일 때
        printf("FinalSpark\n");
        break;
    default:
        break;
    }

    return 0;
}
~~~

### for문과 같이 사용하기
~~~c
#include <stdio.h>

typedef enum _DayOfWeek {    // 열거형 이름은 _DayOfWeek
    Sunday = 0,                  // 초깃값을 0으로 할당
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    DayOfWeekCount               // 열거형 값의 개수를 나타내는 항목 추가
} DayOfWeek;                 // typedef를 사용하여 열거형 별칭을 DayOfWeek로 정의

int main()
{
    // 초깃값은 Sunday, i가 DayOfWeekCount보다 작을 때까지만 반복
    for (DayOfWeek i = Sunday; i < DayOfWeekCount; i++) 
    {
        printf("%d\n", i);
    }

    return 0;
}

~~~