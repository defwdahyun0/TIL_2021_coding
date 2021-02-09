# 숫자와 문자

## 수의 표현

기본적으로 알아야할 것 : 데이터
데이터 타입 : 숫자, 문자... 기타 등등

숫자와 문자를 어떻게 연산하는가만 알아두 됨
이러한 점이 js를 배웠을 때 좋은점!

'''js
<!DOCTYOE html>
<html>
<head>
    <title></title>
</head>
<bode>
<script type="text/javascript">
    alert(1);
</script>
</body>
</html>
'''

alert( ); 문법적인 궁금증은 가질 필요 없다.
중요한 것은 alert( );라고 하면 괄호 안의 값이 경고창에 표현된다.
여기에 집중하기

---

작성한 파일 열기 - demo1.html

정수 -1,0,1,2,3,4....
실수 -2.0,0.222,0.5,1.1,2.0

정수?실수? 정의는 중요하지 않다.
그냥 숫자는 정수, 실수 모두 쓸 수 있다. js에서는 number라고 부른다.

콘솔에서 실습 할 수도 있다

## 수의 연산

### 덧셈 
alert(1+1);
alert(1.1+1.1);
### 곱셈
alert(2*8);
### 연산 함수
Math.pow(3,2); : 객체
Math.round(10.6) : 반올림
Math.ceil(10.2) : 가장 가까운 위의 정수로 올려줌
Math.floor(10.2) : 가장 가까운 아래의 정수로 내려줌
Math.sqrt(9) : 제곱근 구하기
Math.random(); : 랜덤 수 구하기(소수점 0.2345~)
그래서 100*Math.random은 100이하의 난수

Math.round(100*Math.random()); : 합성

## 문자

'''js
<!DOCTYOE html>
<html>
<head>
    <title></title>
</head>
<bode>
<script type="text/javascript">
    alert("coding everybody");
</script>
</body>
</html>
'''

문자를 입력할 때는 **큰따옴표**를 쓴다.

이제 콘솔 사용

alert('coding everybody');
alert("coding everybody");
콘솔에서는 **큰따옴표** **작은따옴표** 모두 가능하지만, 교차로 사용하는 것은 불가능하다.

'' ""는 지금부터 나오는 text는 문자임을 브라우저에게 알려주는 것이다.
alert("coding everybody'");
'를 문자로 인식하고 잘 종료된다.


alert("egoing's coding everybody");
alert('egoing"s coding everybody');
alert('egoing\'s coding everybody');

위는 모두 유효하다.

\' : escape 도망

1
"1"
위 둘은 다른 데이터 형식이다.
1은 숫자, "1"은 문자

typeof로 type을 알 수 있다.
typeof 1, typeof "1"

"1"은 문자열이라고 한다.

"abcde" 여러 개의 문자가 결합되어 있기 때문에 문자들의 모임, 문자열, string이라고 한다.

## 문자연산

### 여러줄의 표시
'''js
<!DOCTYOE html>
<html>
<head>
    <title></title>
</head>
<bode>
<script type="text/javascript">
    alert("coding\neverybody");
</script>
</body>
</html>
'''

\n은 줄바꿈이라는 의미이다.

### 문자 결합
'''js
<!DOCTYOE html>
<html>
<head>
    <title></title>
</head>
<bode>
<script type="text/javascript">
    alert("coding"+" "+"everybody");
</script>
</body>
</html>
'''

1+1 = 2
"1"+"1" = "11"

"coding everybody"
"coding everybody".length : 16

!!!자바스크립트 사전 링크!!!
string.indexof(search)
"code".indexof("c") : 0
"code".indexof("o") : 1
"code".indexof("d") : 2
"code".indexof("e") : 3

---

프로그래밍 입문자에게 가장 익숙한 데이터 형(data type)은 숫자와 문자일 것이다. 이번 시간에는 실제로 가장 많이 사용되는 데이터 형인 문자와 숫자를 프로그래밍에서는 어떻게 표현하고 연산하는지 알아보자.

## 숫자
자바스크립트에서는 큰따옴표나 작은따옴표가 붙지 않은 숫자는 숫자로 인식한다.

```js
alert(1+1);
```
결과 : 2

```js
alert(1.2 + 1.3);
```
결과 : 2.5

곱하기를 할 때는 *(에스터리스크, Asterisk, 키보드 자판 상으로 숫자 8 위)를 사용한다.

```js
alert(2 * 5);
```
결과 : 10

나누기를 할 때는 /(슬래쉬, slash, 키보드 자판 상으로 오른쪽 shift 키 왼쪽)를 사용한다.

```js
alert(6 / 2)
```
자바스크립트에서는 사칙연산 보다 좀 더 복잡한 연산도 지원한다. 좀 더 자세한 내용은 자바스크립트 사전을 참고한다.

```js
Math.pow(3,2);       // 9,   3의 2승 
Math.round(10.6);    // 11,  10.6을 반올림
Math.ceil(10.2);     // 11,  10.2를 올림
Math.floor(10.6);    // 10,  10.6을 내림
Math.sqrt(9);        // 3,   3의 제곱근
Math.random();       // 0부터 1.0 사이의 랜덤한 숫자
```

## 문자
문자는 "(큰 따옴표) 혹은 '(작은 따옴표) 중의 하나로 감싸야 한다. 큰 따옴표로 시작하면 큰 따옴표로 끝나야하고, 작은 따옴표로 시작하면 작은 따옴표로 끝나야 한다. String이라고 한다.

```js
alert("coding everybody");
```
```js
alert('coding everybody');
```
숫자를 따옴표로 감싸면 문자가 된다. 아래는 문자다. typeof는 값의 데이터 형을 알려주는 기능이다.

```js
alert(typeof "1")
```
결과 : string

아래와 같이 따옴표 없는 숫자는 number가 출력된다.

```js
alert(typeof 1)
```
결과 : number

만약 문자열 안에 작은 따옴표나 큰따옴표를 넣고 싶다면 어떻게 해야할까?

```js
alert('egoing's javascript')
```
웹브라우저에서 실행했다면 아무것도 실행되지 않을 것이고, 크롬 개발자 도구와 같은 콘솔에서 실행했다면 아래와 같은 에러 메시지가 출력 될 것이다.


브라우저에서 실습을 하고 있다면 오류 메시지를 표시하지 않기 때문에 불편할 것이다. 구글 크롬 브라우저에서는 Ctrl+Shift+J (윈도우), 커멘트+Alt+J (OSX) 키를 누르면 웹페이지에서 발생한 에러를 보여준다. 파이어폭스에서는 윈도우 기준 Ctrl+Shift+K를 누르면 오류가 표시될 것이다. IE(IE9,10)에서는 F12를 누른 후에 개발자 도구에서 콘솔탭을 누르면 에러 메시지를 확인할 수 있다.
위의 내용은 문법(Syntax) 에러(Error)가 발생했다는 뜻이다. 작은따옴표는 문자열의 구간을 컴퓨터에게 알려주는 기호인데, 기호가 문자 자체로 사용됐기 때문에 컴퓨터 입장에서는 어디서부터 어디까지가 문자열인지 파악 할 수 없게 된 것이다.

아래와 같이 코드를 변경하면 작은따옴표를 문자열 안에 포함시킬 수 있다.

```js
alert('egoing\'s javascript')
```
\를 ' 앞에 위치시키면 ' 를 문자열의 시작과 끝을 구분하는 구분자가 아니라 단순히 문자로 해석하도록 강제 할 수 있다. 이러한 기법을 이스케이프(escape)라고 한다.

## 여러줄의 표시
여러줄을 표시하기 위해서는 아래와 같이 한다. \n는 줄바꿈을 의미하는 특수한 문자다.

```js
alert("안녕하세요.\n생활코딩의 세계에 오신 것을 환영합니다"); 
```

## 문자연산
문자와 문자를 더할 때는 아래와 같이 한다.

```js
alert("coding"+" everybody");
```
결과 : coding everybody

문자의 길이를 구할 때는 문자 뒤에 .length를 붙인다.

```js
alert("coding everybody".length)
```
결과 : 16

그 외에 문자를 이용한 작업 방법은 자바스크립트 사전을 참고한다.

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/4647)