# 함수
함수(function)란 하나의 로직을 재실행 할 수 있도록 하는 것으로 코드의 재사용성을 높여준다.

## 함수의 형식
함수의 형식은 아래와 같다.

```js
function 함수명( [인자...[,인자]] ){
   코드
   return 반환
   값
}
```

## 함수의 정의와 호출
함수는 function 뒤에 함수의 이름이 오고, 소괄호가 따라온다. 소괄호에 인자라는 값이 차례로 들어오는데 이 값은 함수를 호출할 때 함수의 로직으로 전달될 변수다. 인자는 생략 할 수 있다. 함수를 호출 했을 때 실행하게 될 부분이 중괄호 안쪽에 온다.

다음 예제를 보자. 이 함수의 이름은 numbering이고, 내용은 0부터 9까지를 화면에 출력한다.

```js
function numbering(){
    i = 0;
    while(i < 10){
        document.write(i);
        i += 1;
    }   
}
numbering();
```
위의 예제 제일 하단에 아래 구문에 의해서 numbering이라는 이름의 함수가 호출되고 있는 것이다.

```js
numbering();
```
결과는 아래와 같다.

```js
0123456789
```

numbering();을 여러번 실행하면서 그 결과를 살펴보자.

## 함수가 없다면
새창으로 열기
아래 예제를 보자. 이전 시간에 0부터 9까지 출력하는 애플리케이션을 만들었다. 그런데 0부터 9까지를 5번 출력해야 한다면 어떻게 해야할까? 아래와 같이 해야 할 것이다.

```js
var i = 0;
while(i < 10){
    document.write(i);
    i += 1;
}
 
var i = 0;
while(i < 10){
    document.write(i);
    i += 1;
}
 
var i = 0;
while(i < 10){
    document.write(i);
    i += 1;
}
 
var i = 0;
while(i < 10){
    document.write(i);
    i += 1;
}
 
var i = 0;
while(i < 10){
    document.write(i);
    i += 1;
}
```
만약 이것을 1000번 해야 한다면? 각각의 로직이 1000 줄에 육박한다면? 그리고 그 내용을 수정해야 한다면? 암담한 느낌이 드는가? 함수를 사용한다면 이러한 문제를 현저히 줄일 수 있다. 아래의 예제를 보자. 결과는 같지만 로직은 단 한번만 등장한다.

```js
function numbering(){
    var i = 0;
    while(i < 10){
        document.write(i);
        i += 1;
    }   
}
 
numbering();
numbering();
numbering();
numbering();
numbering();
```

**재사용성,유지보수의 용이,가독성**

## 입력과 출력
함수의 핵심은 입력과 출력이다. 입력된 값을 연산해서 출력하는 것이 함수의 기본적인 역할이다. 다음은 함수에서 입력과 출력의 역할을 하는 구문들에 대한 설명이다.

### return
함수 내에서 사용한 return은 return 뒤에 따라오는 값을 함수의 결과로 반환한다. 동시에 함수를 종료시킨다. 아래 내용을 보자. 결과는 egoing과 k8805다.

```js
function get_member1(){
    return 'egoing';
}
 
function get_member2(){
    return 'k8805';
}
 
alert(get_member1());
alert(get_member2());
```
get_member1와 get_member2를 출력(alert)한 결과가 각각 egoing과 k8805인 이유는 함수 내에서 문자열 egoing과 k8805을 return을 하기 때문이다.

return은 결과를 반환하는 것 외에 함수를 중지시키는 역할도 한다. 다음 코드를 보자. 결과는 egoing이다.

```js
function get_member(){
    return 'egoing';
    return 'k8805';
    return 'sorialgi';
}
alert(get_member());
```
k8805와 sorialgi는 출력하지 않았다. 왜 그럴까? 그것은 return 'egoing'을 실행한 후에 함수가 종료되었기 때문이다. return 'k8805' 이하는 어떠한 경우도 실행되지 않는다.

## 인자
인자란?
인자(argument)는 함수로 유입되는 입력 값을 의미하는데, 어떤 값을 인자로 전달하느냐에 따라서 함수가 반환하는 값이나 메소드의 동작방법을 다르게 할 수 있다. 다음 예를보자. 결과는 1,2이다.

```js
function get_argument(arg){
    return arg;
}

alert(get_argument(1));
alert(get_argument(2));
```
5행의 get_argument(1)은 1행에서 3행 사이에 정의된 함수를 실행하는 구문이다. 5행의 1은 get_argument로 1이라는 값을 전달하겠다는 의미다. 이 때 1행에 정의된 (arg) 구문에 의해서 변수 arg의 값으로 숫자 1이 함수 안으로 전달된다. 이 변수 arg는 함수 get_argument 안에서만 유효하다. 이 관계는 아래와 같다.
?

### 복수의 인자
그럼 여러개의 입력 값을 받고 싶다면 어떻게 해야할까? 다음 예제를 보자. 결과는 30과 50이다.

```js
function get_arguments(arg1, arg2){
    return arg1 + arg2
}
 
alert(get_arguments(10, 20));
alert(get_arguments(20, 30));
```

위의 예제를 그림으로 나타내면 아래와 같다. 즉 함수를 호출 할 때 전달한 인자 10과 20은 함수의 선언부(1행)의 arg1, arg2에 차례로 할당된다. 이렇게 전달된 값은 함수 내부로 전달되서 더해진 후에 반환된다.


 
## 함수를 정의 하는 다른 방법
자바스크립트는 함수를 정의하는 또 다른 방법을 제공한다. 다음 예제를 보자. 아래 방법은 함수를 정의 하는 또 다른 방법이다.

```js
var numbering = function (){
    i = 0;
    while(i < 10){
        document.write(i);
        i += 1;
    }   
}
numbering();
```
위의 내용은 이전 예제와 동일 하지만 함수를 정의 하는 방법을 달리한 것이다. 

```js
(function (){
    i = 0;
    while(i < 10){
        document.write(i);
        i += 1;
    }   
})();
```
위는 일회성으로 호출할 때 사용되는 **익명함수**이다.

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/4729)