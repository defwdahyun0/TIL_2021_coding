# 정규표현식
정규표현식(regular expression)은 문자열에서 특정한 문자를 찾아내는 도구다. 이 도구를 이용하면 수십줄이 필요한 작업을 한줄로 끝낼 수 있다. 

정규표현식은 하나의 언어라고 할 수 있다. 그러므로 본 수업에서 정규표현식의 모든 것을 다루는 것은 불가능하다. 본 수업은 아래와 같은 전략을 취하고 있다.

* 1. 입문자에게 정규표현식이 무엇인가에 대한 개념을 알려준다. 초심자에게는 사용법까지 공부하는 것은 무리다. 나중에 문자를 처리해야하는 상황이 생겼을 때 이곳을 찾아오거나 본 수업을 완주했을 때 마지막 단계로 본 수업을 공부한다.
* 2. 정규표현식을 이미 알고 있는 개발자에게는 정규표현식을 자바스크립트에서는 어떻게 사용하는가를 알려준다. 
* 3. 정규표현식 자체에 대한 학습이 필요하다면 [정규표현식 수업](https://opentutorials.org/course/909/5142)을 공부하자.

## 정규표현식 생성
정규표현식은 두가지 단계로 이루어진다. 하나는 컴파일(compile) 다른 하나는 실행(execution)이다. 우선 컴파일부터 알아보자.

## 컴파일
컴파일은 검출하고자 하는 패턴을 만드는 일이다. 우선 정규표현식 객체를 만들어야 한다. 객체를 만드는 방법은 두가지가 있다. **a라는 텍스트를 찾아내는 정규표현식**을 만들어보자.

## 정규표현식 리터럴
```js
var pattern = /a/
```
정규표현식 객체 생성자
```js
var pattern = new RegExp('a');
```
두가지 모두 같은 결과를 만들지만 각자가 장단점이 있다. 

## 정규표현식 메소드 실행
새창으로 열기
정규표현식을 컴파일해서 객체를 만들었다면 이제 문자열에서 원하는 문자를 찾아내야 한다. 
**정규표현식 사용 : 추출,test,치환**

### RegExp.exec()
```js
console.log(pattern.exec('abcdef')); // ["a"] //pattern = /a./일 때는 ["ab"] return한다. .은 그 뒤 한 문자
```
실행결과는 문자열 a를 값으로 하는 배열을 리턴한다.

```js
console.log(pattern.exec('bcdefg')); // null
```
인자 'bcdef'에는 a가 없기 때문에 null을 리턴한다.

### RegExp.test()
test는 인자 안에 패턴에 해당되는 문자열이 있으면 true, 없으면 false를 리턴한다.

```js
console.log(pattern.test('abcdef')); // true
cnosole.log(pattern.test('bcdefg')); // false
```

## 문자열 메소드 실행
문자열 객체의 몇몇 메소드는 정규표현식을 사용할 수 있다. 

### String.match()
RegExp.exec()와 비슷하다.
```js
console.log('abcdef'.match(pattern)); // ["a"]
console.log('bcdefg'.match(pattern)); // null
```

### String.replace()
문자열에서 패턴을 검색해서 이를 변경한 후에 변경된 값을 리턴한다.

```js
console.log('abcdef'.replace(pattern, 'A'));  // Abcdef
```

## 옵션
 정규표현식 패턴을 만들 때 옵션을 설정할 수 있다. 옵션에 따라서 검출되는 데이터가 달라진다.

### i
i를 붙이면 대소문자를 구분하지 않느다.

```js
var xi = /a/;
console.log("Abcde".match(xi)); // null
var oi = /a/i;
console.log("Abcde".match(oi)); // ["A"];
```

### g

g를 붙이면 검색된 모든 결과를 리턴한다.

```js
var xg = /a/;
console.log("abcdea".match(xg)); //["a"]
var og = /a/g;
console.log("abcdea".match(og)); //["a","a"]
```

### 혼합
```js
var ig = /a/ig;
console.log("AabcdeAa".match(ig)); //["A","a","A","a"]
```

## 사례
### 캡처
괄호안의 패턴은 마치 변수처럼 재사용할 수 있다. 이 때 기호 $를 사용하는데 아래 코드는 coding과 everybody의 순서를 역전시킨다.

```js
var pattern = /(\w+)\s(\w+)/;
var str = "coding everybody";
var result = str.replace(pattern, "$2, $1");
console.log(result);
```

### 치환
아래 코드는 본문 중의 URL을 링크 html 태그로 교체한다. 

```js
var urlPattern = /\b(?:https?):\/\/[a-z0-9-+&@#\/%?=~_|!:,.;]*/gim;
var content = '생활코딩 : http://opentutorials.org/course/1 입니다. 네이버 : http://naver.com 입니다. ';
var result = content.replace(urlPattern, function(url){
    return '<a href="'+url+'">'+url+'</a>';
});
console.log(result);
```
결과는 아래와 같다.

```js
생활코딩 : <a href="http://opentutorials.org/course/1">http://opentutorials.org/course/1</a> 입니다. 네이버 : <a href="http://naver.com">http://naver.com</a> 입니다.
```

## 참고
* [생활코딩 정규표현식 수업](https://opentutorials.org/course/909/5142)
* [정규표현식을 시각화](https://regexper.com/)
* [정규표현식 빌더](https://regexr.com/)

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/6580)