# 2. 

## 1. 문자열, 해쉬

### 문자열
* 문자열 자르기, 합치기
* 문자열 파싱
* 문자열 찾기
    * 문자열 치환 
    * 문자열 부분 복사

### 해쉬
: 해시 테이블은 연관배열 구조를 이용하여 키(key)에 결과 값(value)을 저장하는 자료구조이다.

* 장점과 단점
    * 해싱된 키(Hash Key)를 가지고 배열의 인덱스로 사용하기 때문에 **삭입,삭제,검색이 매우 빠르다** 
    * 해시 함수(Hash Function)를 사용하는데 **추가적인 연산이 필요**하다.
    * 적은 데이터 저장시 구현 방식에 따라 연결리스트(Linked List)를 사용하는 경우 오버 헤드의 부담이 생기고, 캐시 효율이 떨어진다.
    * 해시 테이블(Hash Table)의 크기가 유한적이고 해시 함숙(Hash Function)의 특성상 **해시 충돌(Hash Collision)이 발생**할 수밖에 없다.
    * 충돌이 없거나 적으면 O(1)의 상수 시간에 가까워지고, 충돌이 발생하면 할수록 성능은 점점 O(n)에 가까워진다.
* 문제점
    * 해시 충돌(Hash Collision) : 해싱된 키(Hash Key)가 중복되어 해당 버킷(Bucket)에 이미 레코드가 존재하는 현상을 말한다.
    * 오버플로우(Overflow) : 해시 충돌(Hash Collision)이 버킷(Bucket)에 해당된 슬롯(Slot) 수보다 많이 발생하면 더 이상 버킷에 값을 넣을 수 없다. 이러한 현상을 말한다.
    * 클러스터링(Clustering) : 연속된 레코드에 데이터가 몰리는 현상을 말한다.
* 예시 : https://programmers.co.kr/learn/courses/30/lessons/42577

### KMP
정리: https://baeharam.github.io/posts/algorithm/kmp/

### LCS
- 예제 : 백준 9251번 LCS

## 2. 그리디,브루트포스

### 그리디
* greedy: 용심쟁이
또는 탐욕 알고리즘, 매 선택에서 **지금 이 순간 당장 최적인 답**을 선택하여 적합한 결과를 도출하자
- 문제 해결을 위해서 최적의 선택이 어떤 것인지 알아야 함
- 예제: 백준 11047번 동전 0

### 브루트 포스
브루트 포스(brute force)
brute: 무식한, force: 힘 무식한 힘으로 해석할 수 있다.
**완전탐색 알고리즘.** 즉, 가능한 모든 경우의 수를 모두 탐색하면서 요구조건에 충족되는 결과만을 가져온다.
이 알고리즘의 강력한 점은 예외 없이 100%의 확률로 정답만을 출력한다.
- 일반적 방법으로 문제를 해결하기 위해서는 모든 자료를 탐색해야 하기 때문에 특정한 구조를 전체적으로 탐색할 수
있는 방법을 필요로 한다.
- 알고리즘 설계의 가장 기본적인 접근 방법은 **해가 존재할 것으로 예상되는 모든 영역을 전체 탐색하는 방법**이다.
- 예제: 백준 2309번 일곱 난쟁이
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int a[9];
int n=9;
int main(){
    int sum =0;
    for(int i=0; i<n; i++){
        cin >> a[i];
        sum += a[i];
    }
    sort(a,a+n);

    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if(sum-a[i]-a[j]==100){
                for(int k=0;k<n;k++){
                    if(i==k || j==k) continue;
                    cout<<a[k]<<'\n';
                }
                return 0;
            }
        }
    }
}
```

## 3. 정렬
* 내장 함수 sort()를 써서 풀 수도 있겠지만, 코딩 인터뷰 면접 준비를 위해 알아야한다.
* 카운팅 소트 추가적으로 알아야 한다.
* 카운팅 정렬 써야하는 문제는 예제
* 정렬 알고리즘 중 중요한 것만 빠르게 보여주기

### 카운팅 소트
- 예제: 백준 10989번 수 정렬하기3
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main(void){

    ios_base::sync_with_stdio(false); //for
    cin.tie(0);
    cout.tie(0);

    int n;
    cin >> n;

    vector<int> num(n);

    for(int i=0; i<n; i++){
        cin >> num[i];
    }

    sort(num.begin(), num.end());

    for(int j=0; j<n; j++){
        cout << num[j] << "\n";
    }

    return 0;
}
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

#define MAX 10001

using namespace std;

int main(void){

    ios_base::sync_with_stdio(false); //for
    cin.tie(0);
    cout.tie(0);

    int n;
    int input_num = 0;

    cin >> n;
    vector<int> num(MAX);

    for(int i=0; i<n; i++){
        cin >> input_num;
        num[input_num]++;
    }

    for(int j=0; j<n; j++){
        if(num[i]){
            for(int j=0;j<num[i];j++)
                cout << i << "\n";
        }
    }

    return 0;
}
```
### (+)bubble sort
### Insertion
https://www.toptal.com/developers/sorting-algorithms
### Selection
https://www.toptal.com/developers/sorting-algorithms

### Heap,Merge,Quick

#### 힙 소트
* 힙소트는 비주류
* 참조지역성이좋지않음
* 힙,트리자료구조를알아야함
* 디바이드엔 컨쿼 https://coderkoo.tistory.com/7


#### 퀵소트
* 메모리 사용 적고,참조지역성 좋음 * 최악의 경우 O(N^2)
* 디바이드엔 컨쿼 https://coderkoo.tistory.com/7

#### 머지소트
* 최악의 경우도 괜찮다
* 참조지역성의 원리 만족
* 메모리사용을 꽤 많이 해야함
* 디바이드엔 컨쿼 https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html

### Tim sort
Insertion sort와 Merge sort를 결합

최선 시간복잡도 : O(n)
평균 : O(nlogn)
최악 : O(nlogn)

안정적인 두 정렬 방법을 결합했기에 안정적이고, 추가 메모리는 사용하지만 기존의 Merge sort에 비해 적은 추가 메모리를 사용하여 다른 O(n log n) 정렬 알고리즘의 단점을 최대한 극복한 알고리즘.

현재 많은 프로그래밍 언어에서 표준 정렬 알고리즘으로 채택됨.

https://d2.naver.com/helloworld/0315536


## 4. 스택,큐,덱

### 스택

* 특징
    * LIFO (Last In First Out) 구조 : 한 쪽 끝에서만 자료를 넣고 뺄 수 있는 구 
    * 쌓여 있는 접시들로 이해하면 됨
    * 맨 위 요소만 접근할 수 있음
    * 자료가 없을 때 stack underflow, 스택의 크기 이상 stack overflow

* 시간 복잡도
    * 삽입/삭제
    - 원소를 삽입/삭제하는 경우 : O(1)

* 장점
    * 데이터의 삽입과 삭제가 빠르다. (맨 위 원소 접근 O(1))

* 단점
    * 탐색을 하려면 원소를 하나하나 꺼내서 옮겨가면서 해야함 
    * 맨 위의 원소만 접근 가능하다

* 언제 사용할까
    * 재귀 알고리즘에서 유용하게 사용
    * 역추적을 해야할 때 (ex. 문서 작업 시 실행 취소)


- 좀 더 자세한 설명, 스택을 배열로 구현, 스택을 링크드리스트로 구현 https://sycho-lego.tistory.com/23

### 큐

* 특징
    * FIFO(First-In-First-Out) 구조 : 먼저 넣은 데이터가 먼저 나오는 구조
    * 데이터가 삽입(push)되는 곳을 front, 제거(pop)되는 곳을 back이라고 한다.

* 시간복잡도
    * 삽입/삭제
    - 원소를 삽입/삭제하는 경우 : O(1)
  
* 장점
    * 데이터의 삽입/삭제가 빠르다. O(1)

* 단점
    * queue의 중간에 위치한 데이터로의 접근이 어렵다
    * 참고) 배열로 구현했을 때,
    - 선형 큐 : 
        1. Front는 고정, Back을 이동하면서 데이터를 삭제하는 경우: 데이터를 제거했을 때, 나머지 데이터를 한 칸씩 다 옮겨야 함.
        2. 둘 다 이동하면서 삽입, 삭제를 할 경우 : 배열의 끝에 저장되어 있는 상황되면, Back을 더 이상 이동시킬 수 없어서 overflow 발생
        - 순환 큐(환형 큐) : 선형 큐를 보완하기 위한 방식. front가 큐의 끝에 닿으면 큐의 맨 앞으로 자료를 보내서 원형으로 연결.
  
* 언제 사용할까
    * 데이터를 입력된 순서대로 처리해야 할 때
    * BFS(너비 우선 탐색) 구현할 때
 
 ### 덱(Deque)

* 특징
    * Deque(Double Ended Queue)와 비슷하지만 queue는 front에서만 삭제하고,end에서 삽입하는데,
    deque는 front와 end에서 삭제와 삽입이 모두 가능하다.
    * 연속적인 메모리를 기반으로 하는 '시퀀스 컨테이너'이다. 따라서,임의 접근 반복자 제공
    * deque는 새로운 메모리 단위를 할당하여 요소를 추가한다
    * 크기가 가변적이다. (선언 후에 변경할 수 있다.)
    * 중간 요소가 삽입, 삭제될 때, 요소들을 앞/뒤로 밀 수 있으므로 vector보다는 좋은 성능을 갖음. 그래도, 앞/뒤에서의 삽입/삭제 성능은 좋지만 중간에서는 좋지 않다.