# 조건문
## Boolean
'비교 수업'에서 비교 연산의 결과로 참(true)이나 거짓(false)을 얻을 수 있다고 배웠다. 여기서 참과 거짓은 '숫자와 문자 수업'에서 배운 숫자와 문자처럼 언어에서 제공하는 데이터 형이다. 이를 Boolean(불린)이라고 부르고 불린으로 올 수 있는 값은 true와 false 두가지 밖에 없다. 불린은 조건문에서 핵심적인 역할을 담당한다.

## 조건문
조건문이란 주어진 조건에 따라서 에플리케이션을 다르게 동작하도록 하는 것이다.

## 조건문의 문법
### if
조건문은 if로 시작한다. if 뒤의 괄호에 조건이 오고, 조건이 될 수 있는 값는 Boolean이다. Boolean의 값이 true라면 조건이 담겨진 괄호 다음의 중괄호 구문이 실행된다.

아래 예제의 실행결과는 'result : true'다. if 뒤에 true가 왔기 때문이다.

```js
if(true){
    alert('result : true');
}
```

다음 예제는 아무것도 출력하지 않을 것이다. if 뒤에 false가 왔기 때문이다.
```js
if(false){
    alert('result : true');
}
```
다음 예제를 보자. 결과는 12345를 출력할 것이다.

```js
if(true){
    alert(1);
    alert(2);
    alert(3);
    alert(4);
}
alert(5);
```

다음 예제를 실행해보자. 결과는 5만 출력될 것이다.
```js
if(false){
    alert(1);
    alert(2);
    alert(3);
    alert(4);
}
alert(5);
```

왜 그럴까? if 문의 조건이 참이면 중괄호의 시작({}부터 중괄호의 끝(})까지의 구간이 실행되기 때문이다. 거짓이면 중괄호 구간이 실행되지 않기 때문에 alert(5); 구문만 실행된 것이다.

### else
if만으로는 좀 더 복잡한 상황을 처리하는데 부족하다. 아래 예제를 보자. 결과는 1이다.

```js
if(true){
    alert(1);
} else {
    alert(2);
}
```

다음 예제의 결과는 2다.
```js
if(false){
    alert(1);
} else {
    alert(2);
}
```

if문의 조건이 true라면 if의 중괄호 구간이 실행되고, false라면 else 이후의 중괄호 구간이 실행된다. 즉 else는 주어진 조건이 거짓일 때 실행할 구간을 정의하는 것이다.

### else if
else if를 이용하면 조건문을 좀 더 풍부하게 할 수 있다. 아래 예제를 보자. 결과는 2다.

```js
if(false){
    alert(1);
} else if(true){
    alert(2);
} else if(true){
    alert(3);
} else {
    alert(4);
}
```

다음 예제의 결과는 3이다.

```js
if(false){
    alert(1);
} else if(false){
    alert(2);
} else if(true){
    alert(3);
} else {
    alert(4);
}
```

다음 예제의 결과는 4다.

```js
if(false){
    alert(1);
} else if(false){
    alert(2);
} else if(false){
    alert(3);
} else {
    alert(4);
}
```

else if는 좀 더 다양한 케이스의 조건을 검사할 수 있는 기회를 제공한다. else if의 특징은 if나 else와는 다르게 여러개가 올 수 있다는 점이다. else if의 모든 조건이 false라면 else가 실행된다. else는 생략 가능하다.

## 변수와 비교연산자
앞서 배운 변수와 비교연산자 그리고 조건문을 결합해보자. ID의 값으로 egoing을 입력해보고, 다른 값도 입력해보자. 아래의 예제는 브라우저에서 실행해야 한다. 다른 환경에서는 원하는데로 동작하지 않을 것이다.

```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요.')
        if(id=='egoing'){
            alert('아이디가 일치 합니다.')
        } else {
            alert('아이디가 일치하지 않습니다.')
        }
    </script>
</body>
</html>
```

위의 내용에서 prompt() 구문은 사용자가 입력한 값을 가져와서 id 변수의 값으로 대입한다. 이러한 것을 API 또는 함수라고 부르는데, 이에 대한 내용은 곧 배운다. 사용자가 입력한 값이 egoing이라면 '아이디가 일치 합니다'를 출력하고 그렇지 않다면 '아이디가 일치하지 않습니다'를 출력한다.

> prompt : 입력을 받아서 콘솔에 출력함
> alert(prompt('')) : 입력을 받아서 경고창에 출력함

## 조건문의 중첩
위의 예제에서 아이디와 비밀번호를 모두 검증해야 한다면 어떻게 하면 될까? 다음 예제를 보자.

```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요.');
        if(id=='egoing'){
            password = prompt('비밀번호를 입력해주세요.');
            if(password==='111111'){
                alert('인증 했습니다.'+id+"님 반갑습니다.");
            } else {
                alert('인증에 실패 했습니다.');
            }
        } else {
            alert('인증에 실패 했습니다.');
        }
    </script>
</body>
</html>
```

if문 안에 다시 if문이 등장했다. 즉 사용자가 입력한 값과 아이디의 값이 일치하는지를 확인한 후에 일치한다면 비밀번호가 일치하는지 확인한 것이다. 이렇게 조건문은 조건문 안에 중첩해서 사용될 수 있다.

## 논리 연산자
이제 논리 연산자를 알아보자. 논리 연산자는 조건문을 좀 더 간결하고 다양한 방법으로 구사할 수 있도록 도와준다.

### &&
&&는 좌항과 우항이 모두 참(true)일 때 참이된다. 다음 예제를 보자. 결과는 1이다. &&의 좌우항이 모두 true인 것은 첫번째 조건문 밖에 없기 때문이다. 이러한 논리 연산자를 and 연산자라고 한다.

```js
if(true && true){
    alert(1);
}
if(true && false){
    alert(2);
}
if(false && true){
    alert(3);
}
if(false && false){
    alert(4);
}
```
논리 연산자를 이용한 사례를 살펴보자. 다음 예제는 논리 연산자를 이용해서 이전 예제를 개선한 것이다.
```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요.');
        password = prompt('비밀번호를 입력해주세요.');
        if(id=='egoing' && password=='111111'){
            alert('인증 했습니다.');
        } else {
            alert('인증에 실패 했습니다.');
        }
    </script>
</body>
</html>
```
중첩된 if문을 하나로 줄였다. 덕분에 코드의 복잡성도 낮아졌다. &&는 아래와 같은 의미를 만든다.

"id의 값이 egoing이고 password의 값이 111111이면 참이다"

즉 && 연산자의 좌항과 우항이 모두 참일 때 전체가 참이 되는 것이다.

### ||
'||'는 '||'의 좌우항 중에 하나라도 true라면 true가 되는 논리 연산자다. |기호는 통상 엔터키 위에 있는 원화표시 키를 쉬프트와 함께 누르면 입력된다. or 연산자라고 부른다. 다음 예를 보자. 결과는 1,2,3이 출력된다. 마지막 조건문의 '||'는 좌항과 우항이 모두 false이기 때문에 false가 된다.

```js
if(true || true){
    alert(1);
}
if(true || false){
    alert(2);
}
if(false || true){
    alert(3);
}
if(false || false){
    alert(4);
}
```
다음 예제는 id 값으로 egoing, k8805, sorialgi 중의 하나를 입력하면 '인증 했습니다'가 출력되고, 그 외의 값을 입력하면 '인증에 실패 했습니다.'를 출력하는 예제다.

```js
id = prompt('아이디를 입력해주세요.');
if(id==='egoing' || id==='k8805' || id==='sorialgi'){
    alert('인증 했습니다.');
} else {
    alert('인증에 실패 했습니다.');
}
```
위의 예제에서는 논리 연산자를 3개 사용했다. 2개만 사용하는 것이 아니라는 것을 보여주기 위한 예제다.

다음 예제는 id 값으로 egoing, k8805, sorialgi 중의 하나를 사용하고 비밀번호는 111111을 입력하면 right 외의 경우에는 wrong를 출력하는 예다.

```js
id = prompt('아이디를 입력해주세요.');
password = prompt('비밀번호를 입력해주세요.');
if((id==='egoing' || id==='k8805' || id==='sorialgi') && password==='111111'){
    alert('인증 했습니다.');
} else {
    alert('인증에 실패 했습니다.');
}
```
위의 예제에서는 or와 and를 혼합해서 사용하는 방법을 보여준다. id 값을 테스트 하는 구간을 괄호()로 묶었다. 사용자가 id의 값으로 egoing 비밀번호를 111111을 입력했다면 연산의 순서는 아래와 같이 된다.

    * (id=="egoing" or id=="k8805" or id=="sorialgi") : true가 된다.
    * password=='111111' : true가 된다.
    * true(1항) and true(2항) : true가 된다.
id 비교를 할 때 괄호를 사용한 것은 사칙 연산을 할 때 괄호부터 계산하는 것과 같은 원리다.

### !
'!'는 부정의 의미로, Boolean의 값을 역전시킨다. true를 false로 false를 true로 만든다. not 연산자라고 부른다. 아래의 결과는 4다.

```js
if(!true && !true){
    alert(1);
}
if(!false && !true){
    alert(2);
}
if(!true && !false){
    alert(3);
}
if(!false && !false){
    alert(4);
}
```

## boolean의 대체제

### 01
조건문에 사용될 수 있는 데이터 형이 꼭 불린만 되는 것은 아니다. 관습적인 이유로 0는 false 0이 아닌 값은 true로 간주된다. 아래의 예제는 2를 출력한다.

```js
if(0){
    alert(1)
}
if(1){
    alert(2)
}
```

### 기타 false로 간주되는 데이터 형
다음은 false와 0 외에 false로 간주되는 데이터형의 리스트다. if문의 조건으로 !(부정) 연산자를 사용했기 때문에 각 조건문의 첫번째 블록이 실행되는 것은 주어진 값이 false이기 때문이다.

```js
if(!''){
    alert('빈 문자열')
}
if(!undefined){
    alert('undefined');
}
var a;
if(!a){
    alert('값이 할당되지 않은 변수'); 
}
if(!null){
    alert('null');
}
if(!NaN){
    alert('NaN');
}
```

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/4724)