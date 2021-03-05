# 1.

## 알고리즘

### 알고리즘이란?
알고리즘이란 어떠한 문제를 해결하기 위한 여러 동작들의 모임을 말한다. 유한성을 가지며, 언젠가는 끝나야 하는 속성을 가지고 있따. 수학과 컴퓨터 과학에서 알고리즘이란 작동이 일어나게 하는 내재하는 단계적 집합이다. 알고리즘은 연산, 데이터 진행 또는 자동화된 추론을 수행한다.

### 알고리즘의 조건
알고리즘은 다음의 조건을 만족해야 한다.
* 입력: 외부에서 제공되는 자료가 0개 이상 존재한다.
* 출력: 적어도 2개 이상의 서로 다른 결과를 내어야 한다.(즉 모든 입력에 하나의 출력이 나오면 안됨)
* 명확성: 수행 과정은 명확하고 모호하지 않은 명령어로 구성되어야 한다.
* 유한성(종결성): 유한 번의 명령어를 수행 후(유한 시간 내)에 종료한다.
* 효율성: 모든 과정은 명백하게 실행 가능(검증 가능)한 것이어야 한다.

### 효율성과 복잡도
알고리즘의 실행시간을 두 부분으로 나누면

1) 입력값의 크기에 따라 알고리즘의 실행시간을 검증
2) 입력값의 크기에 따른 함수의 증가량, 우리는 이것을 성장률이라고 부른다. 이 때 중요하지 않는 상수와 계수들을 제거하면 알고리즘의 실행시간에서 중요한 성장률에 집중할 수 있는데 이것을 점금적 표기법(Asymptotic notation)이라 부른다.

점근적 표기법은 다음 세가지가 있는데 시간복잡도를 나타내는데 사용된다.
* 최상의 경우: 오메가 표기법
* 평균의 경우: 세타 표기법
* 최악의 경우: 빅오 표기법

평균인 세타 표기를 하면 가장 정확하고 좋겠지만 평가하기가 까다롭다.
그래서 최악의 경우인 빅오를 사용하는데 알고리즘이 최악일 때의 경우를 판단하면 평균과 가까운 성능으로 예측하기 쉬움

### 시간복잡도
시간복잡도의 가장 간단한 정의는 알고리즘의 성능을 설명하는 것
다른 의미로는 알고리즘을 수행하기 위해 프로세스가 수행해야하는 연산 수치화
왜 실행시간이 아닌 연산수치로 판별할까? 명령어의 실행시간은 컴퓨터의 하드웨어 또는 프로그래밍 언어에 따라 편차가 크게 달라지기 때문에 명령어의 실행 횟수만을 고려하는 것이다.

시간복잡도에서 중요하게 보는것은 가장 큰 영향을 미치는 n의 단위이다.

1O(1)->상수
2n+2O O(n)->n이 가장 큰영향을 미친다.
3n^2 O(n^2)->n^2이 가장 큰영향을 미친다.

O(1): 상수
아래 예제처럼 입력에 관계없이 복잡도는 동일하게 유지된다.
printf("Hello");

O(N): 선형
입력이 증가하면 처리 시간 또는 메모리 사용이 선형적으로 증가한다.
```cpp
for(int i=0;i<n;i++)
{
    printf("Hello");
}
```

O(N^2): Square
반복문이 두 번 있는 케이스
```cpp
for(int i=0;i<n;i++)
{
    for(int i=0;i<n;i++)
    {
        printf("Hello");
    }
}
```

### 정렬 알고리즘의 복잡도

공간복잡도: 최악

BubbleSort O(1)
HeapSort O(1)
InsertionSort O(1)
MergeSort O(n) 
QuickSort O(logn)
SelectionSort O(1)
ShellSort O(1)
SmoothSort O(1)

시간복잡도: 최선-평균-최악 순

BubbleSort O(n) O(n^2) O(n^2)
HeapSort O(nlogn) O(nlogn) O(nlogn)
InsertionSort O(n) O(n^2) O(n^2)
MergeSort O(nlogn) O(nlogn) O(nlogn)
QuickSort O(nlogn) O(nlogn) O(n^2)
SelectionSort O(n^2) O(n^2) O(n^2)
ShellSort O(n) O(nlog(n^2)) O(nlog(n^2))
SmoothSort O(n) O(nlogn) O(nlogn)

### 자료구조 복잡도

### 복잡도가 중요한 이유 = 시간초과
- 예제: 백준 1929번 소수 구하기

시간초과
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main(){

    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    int start_num, end_num;

    int i,j;

    cin >> start_num >> end_num;

    for(i=start_num; i<end_num+1; i++){
        for(j=2; j<i; j++){
            if(i%j == 0) break;
        }
        if(i==j)
            cout << i <<"\n";
    }
    return 0;
}
```

시간초과 해결(에라토스테네스의 체)
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

#define MAX_SIZE 1000000
using namespace std;

int main(){

    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    int start_num, end_num;
    bool not_prime+num[MAX_SIZE+5] = {false,};

    not_prime_num[1] = true;

    for(int i=2; i<=MAX_SIZE; i++){
        if(not_prime_num[i] == false){
            for(int j=2; j*i <= MAX_SIZE; j++){
                not_prime_num[j*i] = true; // 소수가 아닌 수
            }
        }
    }

    cin >> start_num >> end_num;

    for(int i=start_num; i<end_num+1; i++){
        if(!not_prime_num[i])
            cout << i <<"\n";
    }
    return 0;
}
```
https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4

### 복잡도 계산
- 입력으로 계산, 정확한 계산은 불가능