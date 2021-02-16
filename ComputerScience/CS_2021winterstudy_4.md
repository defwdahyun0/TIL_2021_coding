# 운영체제

## 1. Deadlock
Deadlock : 교착상태
아무도 제 방향대로 진행을 하지 못하는 상태이다.
진행반향의 차들이 양보를 하려 하지 않아 아무런 차도 나갈 수 없는 상태이다.
동작하는 Process들이 요구하는 리소스(cpu,memory -> critical section -> race condition)
리소스를 사용하고 싶으면 lock을 걸고 보호를 하게 되는데, 둘 다 사용하려 하지 않으면 프로그램이 끝나지 않는 현상이 생기기도 한다.

데드락이 일어나려면? 네 가지 필요조건
하나라도 만족하지 않으면 교착상태는 발생하지 않다.
독립상태는 아니고 다른 하나랑 연결이 되는 경우가 있기 때문에 4가지 알아둬야 한다.

### 1. 상호배제(Mutual exclusion) 

프로세스들이 필요로 하는 자원에 대해 배타적인 통제권을 요구한다.

프로세스가 리소스를 사용할 때 lock을 거는 과정, sync, lock을 거는 행위 자체

### 2. 점유대기 (Hold and wait)
프로세스가 
### 3. 비선점(No preemption)
프리미티브 : 프로세스 웹
프로세스가 동작할 때 중간에 다른 동작이 끼어듬. premitive로 바꾸면 deadlock을 피해갈 수 있따. 
### 4. 순환대기(Cicular wait)

### 5. 추가적인 부분
위 3개로 인해 원인, 모니터, 방지, 회복

## 2. CPU scheduling

메모리 중심으로 컴퓨터가 동작한다. cpu가 메모리에서 프로세스를 빼오는데, 어떤 프로세스를 빼올지에 대한 기준을 제시한다. cpu는 중간에 scheduler가 있는데 cpu가 스케줄러를 짜준다. 
cpu sch 조율할 때 이런 기능을 하지만 기준이 더 중요하다.

아래 3가지가 중요한 기준들이다.
* CPU utilization
: cpu busy-ness

cpu가 기능적인 부분을 담당한다. cpu가 동작하지 않으면 컴퓨터 시스템이 동작할 수 없다. ram이 아니라 cpu가 computing power를 결정한다.
cpu 입장에서 좋다.

* Throughput

몇 초에 몇 번 수행하냐.

* Waiting time

아래는 덜 중요하다. 어느정도 정해져있기 때문이다.
* Turnaround time
* Response time

* Dispatcher
context switching
프로세스가 멀티태스킹 환경에서 하나만 동작하는 것이 아니라 여러 가지가 함꼐 동작하고 있다.
각각의 cpu에서 동작할 수도 있겠지만 마법처럼 속이는 방식
실제로는 넘어가는 과정이 반복된다. 과정에서 이 프로세스를 다른 프로세스로 연결시켜주는 과정을 context switch를 시켜준다.

dispatch. context switch PCB(Process Control Block) 프로세스의 state를 기억해두는 block 역할들을 수행하면서 delay가 발생한다. context switching delay. latency가 많으면 좋지 않다. 프로세스 실행 중간에 텀이 생겨서 많을수록 좋지는 않다.

dispatch에 대한 설명의 이유는 

## cpu 프로세싱 방법 5가지.
### FCFS
First Come First Sub
먼저 온 것부터 처리한다.

 cpu utilization이 p1,p2,p3를 바꾼다고 해서 달라지지 않는다.
30초동안 cpu는 context switching이 일어나서 잠깐 쉬어도 cpu utilization은 변하지 않는다.
 throughput도 똑같다.
스케쥴링을 어떻게 하는지에 따라 throughput이 달라지지는 않는다.
각 프로세스마다 waiting time이 있다.
p2도 ready to에서 
p1은 waiting time 0, p2=24, p3=27
평균은 17

waiting time이 긴 것은 좋지 않다.
단점은 waiting time이 길다.
**convoy effect** : 프로세스 실행 속도는 짧은데 큰놈이 cpu를 차지 하고 있다. 언제까지 기다려야하는지 기약이 없음.

### Shortest-Job-First(SJF)
Convoy effect 피하려면 수행시간이 짧은 것부터 실행한다.
BurstTime 비교!
waiting time이 줄어든다.

단점 
* 예측하기가 어렵다.
예측하는 방법은 이전에 프로세스를 실행했었을 때의 log를 참고해서 예측한다.

premetive : 선점
non-preempitive : 비선점

SJF는 비선점형이다. 침해를 하지 않아서 프로세스가 동시에 들어가있다고 가정하지만, 램 안에서 모든것을 동작하는 것이 아니라 프로세스를 실행하면 arrival time이 존재해서 그런 것을 가정하지 않았다. 


### Shortest-remaining-time-first
SJF와 비슷하지만 그때마다 최신화(Preemptive)
0초 시점이라 했을 때 이전에는 모든 것이 들어 있었음.
0: (p1:8), 1: (p1:8-1, p2:4)
remaining time으로 봤을 때 p2가 들어가게 되고 2단게에서 2초 경에서 p1,p2,p3 들어오고 2: (p1:7, p2:4-1=3, p3:9)
4: (p1:7 p2:2 p3:9 pr:5)

preemptive버전이 아니면 끝날 때에 비교를 다시 해서 실행을 하겠지만, SJF는 최신화한다.

* 단점
    * SJF와 비슷하게 예측 불간으
    * 이론상 좋지만 구현하기 어렵다
    * 보다 많은 disptch latency
    : SJF보다 긴 이유 -> p1이 8초, p2가 4초, p4, p3
    dispatch latency가 context switching, 전환시에 발생한다.
    실질적으로 delay가 없게끔 나와있지만 각 switching마다 delay가 발생하고 있다.

    srtf는 잠깐 멈췄다가 다시 동작하는 부분이 많아서 여러 process에서 dispatch latency가 계속 일어난다. dispatch latency가 커진다.

## Priority Scheduling
우선순위가 여러가지 일 수가 있다!
SJF중 process의 burst time은 길지만 지금 바로 수행해야하는 경우, 중요한 process. 
이럴 때는 priority를 보고 배열알 하는 방심이다.
waiting time은 이럴 경우 고려가 되지 않는다.

문제는 starvation, aging 두 개 모두 알아야한다.
starvation : 기아 상태, burst time은 짧지만 prioty가 낮아 실행시간이 늦춰짐. 그러나 계속해서 prioty가 높은 프로세스들이 들어오는 경우에 계속 늦춰짐. 배가 고픈 상태
solution: aging. priority를 ram에서 보낸 시간에 비례해서 올려주는 형식이다.

### Round Robin(PR) - 중요!!!! 실제 스케줄링 알고리즘으로 많이 사용된다.
위 방법들은 장단점이 많다.

process burst time을 쪼갠다. Quantum size:4. 정한 size만큼 쪼개서 사용한다. 24가 6개로 쪼개지고 나서 FCFS. quantum에 하나만 실행시키고 다른 것들 실행시키자???
p1:24, p2:24, p3:24 + QS: 4.
기본적인 base는 fcfs. 우선 다 6개로 쪼갠다.
P1,P2,P3,P1,P2,P#....
waiting time이 짧다.(재실행) utilization, throughput.
하지만 단점, 정말 많은 Dispatch Latency
process가 실행되는 시간에 비해 짧은 수준이긴 하다. cpu의 dispatch latency가 최적화되어서이다.

## 3. 다른 schedulings

### Multiple-Processor Scheduling: Load Balancing

asymmetric muliprocessing : BOSS

symmetric multiprocessing(SMP) : Currently, most common
문제가 될 만한 것. 이만큼의 일을 하고, 15만큼 일을 하는데 관리가 어렵다. 양심이 있다면 일을 더 받겠지만 ... 그냥 흘러간다.
load balancing이 무너진다.

해결방법이 2가지
2 / 15 / 10 만큼의 일

* (양심이 있는 경우) Pull migration :일을 가져온다.
* (일을 넘겨줄 경우) Push migration : 각 프로세서에 2가지 작업이 포함돼서 상호작용이 돼서 로드 밸런싱을 넘겨준다.

### Real-time scheduling
realtime과 실시간의 차이
실시간은 즉각적인 반응이 예상,리얼타임은 외부환경에 영향을 안받고 일정한 것이 지켜지는 것을 realtime. 이런 realtime을 보장하기 위한 scheduling
bursttime t, deadline d, period p
로켓으로 예를 들면 period는 점화가 반복되는 주기, 그 사이에서 deadline을 지켜줘야한다.
두 개 이상이 겹쳤을 때 스케쥴링 방법?

* Rate montonic
rater period.
최종 발표, 큰 과제. 주간 발표는 반복.
주기가 짧을수록 먼저 수행시키고, 주기가 길면 priority를 낮추자.
치명적 단점. 데드라인 놓침
P1이 P2보다 주기가 짧아 먼저 실행시켰는데, p2에서 데드라인을 맞추지 못했다.

* EDF
데드라인이 빠를수록 priority가 높다.
Deadline 맞춤
## Swapping : 스와핑
프로세스가 실행되기 위해 CPU에서 ram에 접근하기 때문에 ram에 프로세스에 대한 정보들이 있어야 한다. 하지만 ram은 저장공간에 한계가 있다.
지금 excuting 시킬 프로세스를 골라서 메인메모리에 넣고, 사용하지 않는 프로세스를 제외할 필요가 있다.
backing store는 hpp, ssd. 이런 프로세스들이 main memory에 올라왔을 때 swap in, swap out

### paging : 매우 중요하다
표준 스와핑을 잘 사용하지 않는다.프로세스 자체를 swapin, swapout. cpu가 있으면 동작시킬건데 멀티태스킹으로 할거라서 . 이 부분을 실행시킬 때 앞부분은 필요가 없기 때문에 조각들만 이동하면 프로세스 하나하나 채울 필요 없이 프로세스 어느정도 정보를 가지고 동작을 하면 되지만 한계가 있는 메모리의 다른 페이지를 채울 수 있다. 프로세스를 페이지 단위로 쪼개서 왔다갔다.
메모리 중심 설명에서 어폐, 프로세스 단위로 들어가지는 않는 이유가 paging. 자체가 들어가는 것이 아니라 page가 들어가서 사용하고 반환하는 것을 반복함.

### Dynamic storage allocation
프로세스가 스와핑. storage 용량 메모리에 대한 allocation은 어떻게
hole의 크기에 따라 가장 큰 hole을 할당한다.
first tie. hole의 최초. 스택마냥 하나씩 채워지는 모습.
Best fit. 홀이 두 가지. 두 가지의 용량에 맞춰서 가장 근사한 것으로 hole에 프로세스를 할당해준다. worst fit은 가장 큰 hole을 할당한다.

문제: fragmentation
externalfragmentation. 중간에 비는 이유. 중간에 비지 않는 프로세스가 할당해서 사용. best fit으로 넣어뒀는데 빈공간이 생길 수가 있다.
외부 단가. 사용가능한 메모리가 300MB, 요청된 메모리가 298. 이론상으로는 더 작기 때문에 사용할 수 있지만 실제로는 사용하지 못한다.
작은 다수의 hole이 생긴다. 중대한 문제. 해결 기법이 compaction. 작은 메모리들을 한 데 모아서 300mb공간. 이 공간은 사용않아고 segmentation, paging

exteranal , internal.
바이트에 할당했을 때 조금의 hole이 발생하는 현상
남은 2바이트 크기의 hole. 남은 2바이트는 낭비

compaction 해결방법이 있지만 사용 않아고, segmentation, paging.

segmentation은 process를 단위를 기준으로 쪼개는 것이다. (아까는 그 자체로 들어감) 논리적으로 이해. 쪼갠 것들을 segmentation table에 따라서 넣어준다. 쪼갠 크기가 다를 것이다. 기능적인것을 기준으로 sort. 

paging도 쪼개는 것이다. 기능별로 쪼개는 것이 아니라 page 크기를 frame이나 page 크기에 따라서 쪼개서 physical memory에 넣어준다. Logical memory는 virtual memory. 그 사이에서 segmentation table이 있듯이 page table 정보를 조회해서 동작을 시키는 구조이다. 

비교
고정된 영역을 분할하는 page.
segmentation은 기능에 따라 가변적으로 분할
이런 차이로 인해 segmentation은 외부 단편화는 발생, 내부 단편화는 발생하지 않는다.

paging에서 외부 단편화가 발생하지 않는 이유 : 프레임 단위랑 페이지 단위를 같게 하면 페이지가 없어져도 같은 사이즈로 재할당이 가능해서 공간이 비는 현상이 일어나지 않는다. 외부 단편화는 생기지 않는다.

segmentation이 가변적. segmentation에 따라 크기가 달라서 기능적으로 했을 때 정확하게 넣어서 내부적으로 단편화 발생 page(frame).


## 4. Main Memory

* segmentation fault란? 
하용되지 않는 메모리 영역에 접근을 시도.

cpu가 physical 메모리에서 꺼내온다. zoom을 쪼갠다고 생각하면 segment0부분을 실행시켜야하는데 이 부분이 없다. 프로세스 자체를 올려놓으면 있는데 쪼개면서 없어지는 경우가 많다. cpu가 실행시켜야하는데 없다. segmentation fault. ram에 없다.

에러 자체는 page fault가 맞는 표현이다. 

어느정도는 사용하기도 한다.

* Page fault
demanding paging.

추가 : Paging with TLB


## 5. Virtual Memory
-> 강의 다시 듣기

keywords!

* virtual memory 사용 이유
: virtual memory

cpu mm(ram) vm

가상메모리를 사용하는 오버워치 입장에서는 vm를 보고 4gb네. 하고 사용을 할 수 있게 된다. vm에 오버워치 프로세스. 다 바로 사용하는게 아니라 paging을 통해서 사용할 친구만 집어넣어 돌리고 빠르게 넣고 빼고.

* demanding paging
* page fault
* page Replace Alogorithm
    * FiFO
    * Optional



