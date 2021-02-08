# 반복문
loop, iterate
## 반복문
인간은 반복적인 작업을 잘하지 못한다. 실수하고, 지루해한다. 컴퓨터는 이런 반복적인 작업을 대행하기 위해서 만들어진 기계다. 반복문은 컴퓨터에게 반복적인 작업을 지시하는 방법이다.

## 반복문의 문법
반복문의 문법은 몇가지가 있다. 각각의 구문은 서로 대체 가능하기 때문에 상황과 취향에 따라서 선택해서 사용하면 된다.

### while
형식은 아래와 같다.

```js
while (조건){ //boolean, true->false
    반복해서 실행할 코드
}
```

아래의 예제를 실행해보자.
```js
다음 예제는 무한반복을 발생시킨다. 저장되지 않은 작업이 있다면 모두 정리한 후에 이 명령을 실행하자. 웹브라우저는 무한반복을 허용하지 않기 때문에 어느 정도 시간이 흐르면 스크립트를 종료할 것인지 물어볼 것이다.
```
```js
document.write는 자바스크립트를 이용해서 웹페이지에 텍스트를 출력한다. 이것은 웹브라우저에서만 동작할 것이다. node.js 콘솔과 같은 환경에서 실습을 한다면 console.log와 같은 메소드를 대신 사용한다.
```
```js
while(true){
    document.write('coding everybody <br />');
}
```
이번에는 true를 false로 바꾼 아래의 예제를 실행해보자. 아무런 결과도 출력하지 않을 것이다.

```js
while(false){
    document.write('coding everybody <br />');
}
```
while문은 while문 뒤에 따라오는 괄호 안의 조건이 참(true)면 중괄호 안의 코드 구간을 반복적으로 실행한다. 조건이 false면 반복문이 실행되지 않는다. 여기서 true와 false는 종료조건이 되는데, 이 값을 변경하는 것을 통해서 반복문을 종료시킬 수 있다. 반복문에서 종료조건을 잘못 지정하면 무한반복이 되거나, 반복문이 실행되지 않는다.

이번 수업의 초입에서 살펴본 반복문의 문법을 해석해보자. 아래의 반복문은 i의 값을 1씩 순차적으로 증가시킴으로서 반복의 지속 여부를 결정하고 있다. 주석으로 첨부한 설명을 주의깊게 살펴보자.

```js
var i = 0;
// 종료조건으로 i의 값이 10보다 작다면 true, 같거나 크다면 false가 된다.
while(i < 10){
    // 반복이 실행될 때마다 coding everybody <br />이 출력된다. <br /> 줄바꿈을 의미하는 HTML 태그
    document.write('coding everybody'+i+'<br />');
    // i의 값이 1씩 증가한다.
    i++
}
```

## for
형식은 아래와 같다.

```js
for(초기화; 반복조건; 반복이 될 때마다 실행되는 코드){
    반복해서 실행될 코드
}
```
다음 예제를 보자.

```js
for(var i = 0; i < 10; i++){
    document.write('coding everybody'+i+'<br />');
}
```

for문은 제일 먼저 '초기화'를 한다. 위의 예제에서 초기화는 var i = 0;이다. 즉 변수 i의 값을 0으로 설정한 것이다. 그 다음에는 '반복조건'인 i < 10이 실행된다. 현재 i의 값은 0이다. 그렇기 때문에 이 조건은 참이다. 반복조건이 참이면 중괄호 안의 내용이 실행된다. i의 값이 0이기 때문에 'coding everybody0<br />'이라는 텍스트가 출력된다. '반복해서 실행될 코드'의 실행이 끝나면 '반복이 될 때마다 실행되는 코드'가 실행된다. i++는 현재 i의 값에 1을 더하라는 의미다. 현재 i의 값은 0이다. 따라서 i++의 결과로 i는 1이 되었다. 그리고 '반복조건'이 실행된다. 현재 i의 값은 1이기 때문에 i < 10은 참이다. 다시 '반복해서 실행될 코드'가 실행된다. 그렇게 반복해서 작업이 실행된다. 이 과정에서 i의 값은 반복 할 때마다 1씩 증가한다. 결국 i의 값이 10이 되는 순간 i < 10을 충족시키지 못하게 되고 반복문은 종료된다.

>> i++ : 0,1,2,3...
>> ++i : 1,2,3,4...
## 반복문이 없다면
coding everybody를 10번 반복해서 출력하고 싶다고 한다면 아래와 같이 코드를 작성하면 된다.

```js
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
document.write('coding everybody');
```
이 정도의 작업은 복사&붙여넣기를 이용해서도 할만하다. 하지만 좀 더 큰 규모의 데이터를 다뤄야 한다면 반복문의 효용이 부각되기 시작한다. 예를들어서 'coding everybody'를 1천번 출력해야 한다면 위의 예제와 아래 예제의 코드 분량에 큰 차이가 생길 것이다.

```js
var i = 0;
while(i < 10){
    document.write('coding everybody <br />');
    i++;
}
```
만약 반복문 없이 coding everybody 뒤에 숫자를 1부터 10까지 붙이고 싶다면 아래와 같이 코드를 작성해야 할 것이다. 행마다 숫자를 바꿔야 하기 때문에 Copy & Paste도 할 수 없다.

```js
document.write('coding everybody 1<br />')
document.write('coding everybody 2<br />')
//중략
document.write('coding everybody 9<br />')
document.write('coding everybody 10<br />')
```
반복문에서는 아래와 같이 하면 된다.
```js
var i = 0;
while(i < 10){
    document.write('coding everybody '+i+'<br />');
    i++;
}
```
coding everybody 뒤에 붙는 숫자를 2의 배수하고 싶다면 어떻게 해야할까? 반복문이 없다면 한줄 한줄 수정해야 할 것이다. 반복문에서는 아래와 같이 내용을 조금만 변경하면 된다.
```js
var i = 0;
while(i < 10){
    document.write('coding everybody '+(i*2)+'<br />');
    i++;
}
```

## 반복문의 제어
### break
반복작업을 중간에 중단시키고 싶다면 어떻게 해야할까?  break를 사용하면 된다. 아래의 예제는 위에서 살펴본 예제를 일부 변형한 것이다.
```js
for(var i = 0; i < 10; i++){
    if(i === 5) {
        break;
    }
    document.write('coding everybody'+i+'<br />');
}
```
위 코드의 결과는 아래와 같다.
```js
coding everybody 0
coding everybody 1
coding everybody 2
coding everybody 3
coding everybody 4
```
종료조건에 따르면 10행이 출력돼야 하는데 5행만 출력되었다. 2행의 if(i === 5) 에 의해서 i의 값이 5일 때 break 문이 실행되면서 반복문이 완전히 종료된 것이다. 반복문 안에서 break가 실행되면 반복문을 즉시 종료시키는 것이다.

### continue
그럼 실행을 즉시 중단 하면서 반복은 지속돼게 하려면 어떻게 해야 할까? 설명이 어렵다면 예제를 보자. 이전 예제의 break를 continue로 변경했을 뿐이지만 결과는 전혀 다르다.

```js
for(var i = 0; i < 10; i++){
    if(i === 5) {
        continue;
    }
    document.write('coding everybody'+i+'<br />');
}
```
결과는 아래와 같다. 숫자 5가 보이지 않는다. 왜 그럴까? i의 값이 5가 되었을 때 실행이 중단 됐기 때문에 continue 이후의 구문이 실행되지 않은 것이다. 하지만 반복문은 중단되지 않았기 때문에 나머지 결과가 출력된 것이다.
```js
coding everybody 0
coding everybody 1
coding everybody 2
coding everybody 3
coding everybody 4
coding everybody 6
coding everybody 7
coding everybody 8
coding everybody 9
```

## 반복문의 중첩
반복문 안에는 다시 반복문이 나타날 수 있다. 다음 예제를 보자. 다음 예제는 00, 01, 02....99 까지를 화면에 출력한다.

```js
// 0부터 9까지 변수 i에 순차적으로 값을 할당        
for(var i = 0; i < 10; i++){
    // 0부터 9까지의 변수를 j의 값에 순차적으로 할당
    for(var j = 0; j < 10; j++){    
        // i와 j의 값을 더한 후에 출력
        // String은 숫자인 i와 j의 데이터 타입을 문자로 형태를 변환하는 명령이다. 
        // String()을 제거하고 실행해보면 의미가 좀 더 분명하게 드러날 것이다.
        document.write(String(i)+String(j)+'<br />'); // i,j로 입력해도 자동으로 문자로 변환해서 연결한다
    }
}
```
```js
단순히 글자를 반복적으로 출력하기 위해서 반복문을 사용한다고 생각 할 수도 있다. 하지만 반복문의 진가는 배열과 결합했을 때 나타난다. 다음 토픽인 배열에서 반복문의 진가를 살펴보자.
```

디버거에 대한 개론. 디버거를 이용하면 코드 중간에 값을 확인할 수 있다.
## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/4728)