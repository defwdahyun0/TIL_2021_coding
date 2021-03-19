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
    * AVL트리는 Adelson-Velskii와 Landis에 의해 1962년에 제안된 트리로서 각 노드에서 왼쪽 서브 트리의 높이와 오른쪽 서브 트리의 높이 차이가 1이하인 이진 탐색 트리
    * AVL 트리는 트리가 비균형 상태로 되면 스스로 노드들을 재배치하여 균형 상태로 만든다. 따라서 AVL트리는 균형 트리가 항상 보장되기 때문에 탐색 시간이 O(log2n) 시간안에 끝나게 됨
    * https://randerson112358.medium.com/avl-trees-a7b4f1fa2d1a

* 전 이진트리(Full), 완전 이진 트리(Complete), 포화이진 트리(Perfect)

* 완전 이진 트리
    * 힙(Heap)은 완전 이진 트리(COmplete binary tree)의 일종


## 특징


## Binary Tree
힙(Heap)은 완전 이진 트리(Complete binary tree)

* 이진 트리(Binary Tree)
    * 각 노드가 최대 두 개의 자식을 갖는 트리
    * 모든 트리가 이진 트리는 아니다.
    * 이진 트리 순회
        1. 중위 순회(in-order traversal)
        2. 전위 순회(pre-order traversal)
        3. 후위 순회(post-order traversal)

* 이진 탐색 트리(Binary Search Tree)

* Balanced Tree
: 트리마다 기준이 조금씩 다르다.


* AVL 트리
**왼쪽 서브트리의 높이와 오른쪽 서브트리의 높이의 차이가 1 이하인 이진 탐색 트리**

* 전 이진 트리 vs 완전 이진 트리 vs 포화 이진 트리
전 : 자식이 없거나 다 채워져 있다.
포화 : 완결
complete : 

* 완전 이진 트리
**마지막 레벨을 제외하고 모든 레벨이 완전히 채워져 있는 트리**
**마지막 레벨은 노드가 왼쪽에서 오른쪽으로 채워져야한다.**
배열 사용

* 힙
**완전이진트리의 일종**으로 **우순순위 큐**를 위해 만들어짐
**최댓값 최솟값**

* 힙의 종류 - 2가지
- 최대힙
- 최소힙
(그림 화살표 의미 x)

알아야할 것 : root가 우선순위 높음 (..)

* 힙-힙의 구현 : 생성
- 힙을 구현할 때는 배열을 쓰는 것이 좋다
- 왼쪽 자식노드 2n 오른쪽 2n+1

* 힙-힙의 구현 : 삽입
insert()
push()
동일한 값은 굳이 바꿀필요 없음

## 우선순위 큐 - 
tree->완전이진트리->힙->우선순위큐


## 백트래킹 - 완전 탐색의 일종 + DFS 간단하게 보기

## 백트래킹 - 모든 경로를 탐색할 때 효율적으로?
막혔을 때 돌아가서 쓸모없는 노드 탐색 안해도 됨

DFS - 깊이 먼저 탐색해서 분별을 빠르게 함 백트래킹 유리
BFS - 가지치기, 프로미싱