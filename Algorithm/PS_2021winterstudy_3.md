# 3.

## 힙 - Heap 이전의 Tree

* 힙(Heap)은 완전 이진 트리(Complete binary tree)의 일종

* 트리는 노드로 이루어진 자료구조
* 루트 노드는 0개 이상의 자식 노드를 갖고 있음
* 자식 노드 또한 0개 이상의 자식 노드를 갖고 있음
    * 반복적으로 정의됨
* 노드간 연결은 edge
* 트리는 그래프의 한 종류
    * 사이클(cycle)이 없는 하나의 연결 그래프(Connected Graph)
    * DAG(Directed Acyclic Graph, 방향성이 있는 비순환 그래프)의 한 종류
* **Root-edge-node1,node2,node3..**

* 최소 연결 트리
* 트리는 계층 모델
* DAG(Directed Acyclic Graph)
    * loop나 circuit이 없음
    * 즉, 사이클이 없음
* 노드가 N개인 트리는 항상 N-1개의 edge를 가짐
* 루트에서 어떤 노드로 가는 경로는 유일함
    * 임의의 두 노드 간의 경로도 유일함
* 한 개의 루트 노드만이 존재하며
    * 모든 자식 노드는 한 개의 부모 노드만을 가짐

* 힙(Heap)은 완전 이진 트리(Complete binary tree)의 일종

* 이진트리(Binary Tree)
    * 각 노드가 최대 두 개의 자식을 갖는 트리
    * 모든 트리가 이진 트리는 아니다.
    * 이진 트리 순회(https://hongku.tistory.com/160)
        * 1. 중위 순회(in-order traversal)
        * 2. 전위 순회(pre-order traversal)
        * 3. 후위 순회(post-order traversal)

* 이진 탐색 트리(Binary Search Tree)
    * 모든 노드가 왼쪽과 같은 규칙을 가진 이진트리
    * 모든 왼쪽 자식들은 현 부모 노드보다 작고
    * 모든 오른쪽 자식들은 현 부모 노드보다 큼

* Balanced Tree
    * O(logN) 시간에 insert와 find를 할 수 있을 정도로 균형이 잘 잡혀 있는 경우
    * 균형있는 트리. 이를 Balanced Tree라고 하며, 기존 트리에서 더 발전된(균형을 잡아주는) 트리 종류는 다음과 같다.
        * AVL Tree
        * B Tree
            * https://wangin9.tistory.com/entry/B-tree-B-tree
        * 2-3 Tree
        * 2-3-4 Tree
        * Red-Black Tree

* Balanced Tree: AVL
    * AVL트리는 Adelson-Velskii와 Landis에 의해 1962년에 제안된 트리로서 **각 노드에서 왼쪽 서브 트리의 높이와 오른쪽 서브 트리의 높이 차이가 1이하인 이진 탐색 트리**
    * AVL 트리는 트리가 비균형 상태로 되면 스스로 노드들을 재배치하여 균형 상태로 만든다. 따라서 AVL트리는 균형 트리가 항상 보장되기 때문에 탐색 시간이 O(log2n) 시간안에 끝나게 됨
    * https://randerson112358.medium.com/avl-trees-a7b4f1fa2d1a

* 전 이진트리(Full), 완전 이진 트리(Complete), 포화이진 트리(Perfect)

* 완전 이진 트리
    * 힙(Heap)은 완전 이진 트리(COmplete binary tree)의 일종
    * 트리의 모든 높이에서 노드가 꽉 차 있는 이진 트리.
        * 즉, **마지막 레벨을 제외하고 모든 레벨이 완전히 채워져 있다.**
    * 마지막 레벨은 꽉 차 있지 않아도 되지만 노드가 왼쪽에서 오른쪽으로 채워져야 한다.
    * 완전 이진 트리는 배열을 사용해 효율적으로 표현 가능하다.

* 힙
    * 완전 이진 트리의 일종으로 **우선순위 큐를 위해 만들어진 자료구조**
    * 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조
    * 힙은 일종의 반 정렬 상태(느슨한 정렬 상태)를 유지한다.
    * 간단히 말하면 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰(작은) 이진 트리
    * 힙 트리에서는 중복된 값을 허용한다.
        * (이진 탐색 트리에서는 중복된 값을 허용하지 않는다.)

* 최대 힙(max heap)
    * 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
    * key(부모 노드) >= key(자식 노드)
* 최소 힙(min heap)
    * 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
    * key(부모 노드) <= key(자식 노드)

* 힙의 구현: 생성
    * 힙을 저장하는 표준적인 자료구조는 **배열(속도)**
    * 구현을 쉽게 하기 위하여 배열의 첫 번째 인덱스인 0은 사용되지 않음
    * **특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않음.**
    * 힙에서의 부모 노드와 자식 노드의 관계
        * 왼쪽 자식의 인덱스 = (부모의 인덱스)*2
        * 오른쪽 자식의 인덱스 = (부모의 인덱스)*2 + 1
        * 부모의 인덱스 = (자식의 인덱스)/2
    * 힙에서 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입, 새로운 노드를 부모 노드들과 교환해서 성질 만족

* 힙의 구현: 삭제
    * 최대 힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제
        * 최대 힙(max heap)에서 삭제 연산은 최댓값을 가진 요소를 삭제하는 것
    * 삭제된 루트 노드에는 힙의 마지막 노드를 가져옴
    * 힙을 재구성

* 우선순위 큐 - Priority + Queue
    * 정리하면 Tree -> 완전 이진 트리 -> 힙 -> 우선순위 큐
    * 힙의 특징: 우선순위 큐의 특징
        * 최대 높이 번, 즉 O(logN)번까지만 수행되므로
        * push의 시간복잡도는 O(logN)
    * First in-First Out + 우선순위가 있는 큐
    * 관련 문제 많음 -> 예제 준비
    * 다익스트라 시간 최적화
        * 간단히 구현하면 시간 복잡도가 O(V^2)
        * 우선순위 큐 사용 시 시간 복잡도 O(ElogV)

- 예제: 백준 15552번 최대 힙
```cpp
#include <iostream>
#include <queue>

using namespace std;

int n;
priority_queue<int> pq;

int main(){
    
    cin >> n;
    for(int i=0; i<n; i++){
        int input_operation;
        cin >> input_operation;
        if(input_operation == 0){
            if(pq.empty())
            {
                cout << "0" << "\n";
            }
            else {
                cout << pq.top() << "\n";
                pq.pop();
            }
        } else {
            pq.push(input_operation);
        }
    }
    return 0;
}
```
```cpp
#include <iostream>
#include <queue>

using namespace std;

int main(){
    
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    int n;
    cin >> n;
    priority_queue<int> pq;

    for(int i=0; i<n; i++){
        int input_operation;
        cin >> input_operation;
        if(input_operation == 0){
            if(pq.empty())
            {
                cout << "0" << "\n";
            }
            else {
                cout << pq.top() << "\n";
                pq.pop();
            }
        } else {
            pq.push(input_operation);
        }
    }
    return 0;
}
```

* 백트래킹
    * 완전 탐색의 일종
    * 모든 경로를 탐색할 때 효율적으로 탐색
    * 백트래킹의 기본 아이디어는 '가능한 모든 방법을 탐색한다'
    * 대표적인 완전 탐색 방법으로는 DFS(Depth Fisrt Search, 깊이 우선 탐색)
        * DFS는 모든 곳을 방문하기 때문에 목표지점이 있지 않는 경로로 빠져서 비효율적인 결과를 초래할 수도 있음
    * 비효율적인 경로를 차단하고 목표로 갈 수 잇는 가능성이 있는 루트를 검사하는 방법이 백트래킹 알고리즘
    * 백트래킹은 DFS에 가지치기(Pruning)를 통해 가도 되지 않는 루트는 배재할 수 있음
        * Pruning: 조건에 맞지 않는 루트를 포기하고 다른 루트로 방향을 옮겨 탐색 시간을 절약하는 기법
        * Pruning을 얼마나 잘하느냐에 따라서 효율이 극대화 될 수 있는 방법
        * Promising: 확인 단계에서 해당 루트가 조건에 맞는지를 검사하는 기법(유망한 지)
    * 백드래킹의 대표 예제: n-queen

    * 막혔을 때 돌아가서 쓸모없는 노드 탐색 안해도 됨
        * DFS - 깊이 먼저 탐색해서 분별을 빠르게 함 백트래킹 유리
        * BFS - 가지치기, 프로미싱

- 백준 N-Queen
```cpp
#include <iostream>
#include <vector>

using namespace std;

int n;
int col[15];
int degree_of_metheds = 0;

bool is_promising(int i)
{
    for(int j=0; j<i; j++)
    {
        if(col[j] == col[i] || abs(col[i]-col[j])==(i-j))
            return false;
    }
    return true;
}

void dfs_with(int i)
{
    if(i==n){
        degree_of_methed += 1;
        /*for(int a=0;a<N;a++)
            cout << col[a] << " ";
        cout << "\n";*/
    }
    else
    {
        for(int j=0; j<n; j++)
        {
            col[i]=j;
            if(is_promising(i))
                dfs_with(i+1);
        }
    }
}

int main(){
    
    cin >> n;
    dfs_with(0);
    cout << degree_of_metheds << "\n";
    return 0;
}
```