# 모듈

프로그램은 작고 단순한 것에서 크고 복잡한 것으로 진화한다. 그 과정에서 코드의 재활용성을 높이고, 유지보수를 쉽게 할 수 있는 다양한 기법들이 사용된다. 그 중의 하나가 코드를 여러개의 파일로 분리하는 것이다. 이를 통해서 얻을 수 있는 효과는 아래와 같다.

    * 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용할 수 있다.
    * 코드를 개선하면 이를 사용하고 있는 모든 애플리케이션의 동작이 개선된다.
    * 코드 수정 시에 필요한 로직을 빠르게 찾을 수 있다.
    * 필요한 로직만을 로드해서 메모리의 낭비를 줄일 수 있다.
    * 한번 다운로드된 모듈은 웹브라우저에 의해서 저장되기 때문에 동일한 로직을 로드 할 때 시간과 네트워크 트래픽을 절약 할 수 있다. (브라우저에서만 해당)

## 모듈이란
순수한 자바스크립트에서는 모듈(module)이라는 개념이 분명하게 존재하지는 않는다. 하지만 자바스크립트가 구동되는 호스트 환경에 따라서 서로 다른 모듈화 방법이 제공되고 있다. 이 수업에서는 자바스크립트의 대표적인 호스트 환경인 웹브라우저에서 로직을 모듈화하는 방법에 대해서 알아볼 것이다.

### 호스트 환경이란?

호스트 환경이란 자바스크립트가 구동되는 환경을 의미한다. 자바스크립트는 브라우저를 위한 언어로 시작했지만, 더 이상 브라우저만을 위한 언어가 아니다. 예를들어 node.js는 서버 측에서 실행되는 자바스크립트다. 이 언어는 자바스크립트의 문법을 따르지만 이 언어가 구동되는 환경은 브라우저가 아니라 서버측 환경이다. 또 구글의 제품 위에서 돌아가는 Google Apps Script 역시 자바스크립트이지만 google apps script가 동작하는 환경은 구글 스프레드쉬트와 같은 구글의 제품 위이다. 여러분은 자바스크립트의 문법을 이용해서 PHP와 같은 서버 시스템을 제어(node.js)하거나 구글의 제품(Google Apps Script)을 제어 할 수 있다. 지금 당장은 어렵겠지만, 언어와 그 언어가 구동되는 환경에 대해서 구분해서 사고 할 수 있어야 한다. 이를 위해서는 다양한 언어를 접해봐야 한다.
모듈을 만드는 방법을 알아보기에 앞서서 모듈이 없는 상황을 가정해보자.

## 모듈이 없다면
우선 모듈이 없는 애플리케이션을 하나 만들어보자. 파일의 이름은 main.html 이다.

```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
</head>
<body>
    <script>
        function welcome(){
            return 'Hello world'
        }
        alert(welcome());
    </script>
</body>
</html>
```
위의 코드는 아무런 문제가 없다. 하지만 welcome 함수가 자주 사용되는 것이라고 가정해보자. 이런 경우 이것이 필요할 때마다 이 함수를 정의해서 사용하는 것은 유지보수도 어렵고 낭비가 될 것이다. 이럴 때 모듈이 필요하다. 함수 welcome을 모듈로 만들어보자.

## 모듈의 사용
새로운 파일을 만든다. 이름은 greeting.js 다. 자바스크립트 파일은 확장자로 js를 사용한다.

greeting.js
```js
function welcome(){
    return 'Hello world';
}
```
main.html의 내용을 다음과 같이 변경한다.

main.html
```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
    <script src="greeting.js"></script>
</head>
<body>
    <script>
        alert(welcome());
    </script>
</body>
</html>
```
이전 예제와 비교했을 때 결과는 같다. 하지만 함수 welcome을 main.html의 외부 파일로 분리했다. 다음은 위의 코드에 대한 분석이다.
```js
<script src="greeting.js"></script>
```

JavaScript와 HTML은 완전히 다른 문법을 가진 언어다. 그런데 HTML 문서 안에는 JavaScript와 HTML이 동시에 표현된다. 따라서 브라우저에게 어디서부터 어디까지가 JavaScript이고, HTML인지를 구분해서 알려줘야 한다. 이 역할을 하는 HTML 태그가 script 태그다. script 태그 안쪽에 위치하는 컨텐츠는 브라우저에 의해서 JavaScript로 인식된다. 그런데 위의 코드는 컨텐츠 대신에 src 속성이 있다. 브라우저는 src 속성에 있는 파일을 다운로드해서 실행시킨다. **greeting.js에는 함수 welcome가 정의되어 있기 때문에 main.html 안에 이 함수가 정의 되어 있지 않음에도 실행할 수 있는 것이다**.

## Node.js에서의 모듈의 로드
본 수업은 Node.js를 위한 수업이 아니기 때문에 Node.js를 실행하는 방법은 다루지 않는다. 호스트 환경에 따라서 모듈을 로드하는 방법이 달라진다는 것을 보여주기 위한 예제일 뿐이기 때문에 동영상 수업을 참고하자.
모듈을 로드하는 방법은 호스트 환경에 따라서 달라진다. Node.js에서는 아래와 같은 방법으로 모듈을 로드한다.

node.circle.js (로드될 대상)
```js
var PI = Math.PI;
  
exports.area = function (r) {
return PI * r * r;
};
  
exports.circumference = function (r) {
return 2 * PI * r;
};
```
node.demo.js (로드의 주체) **require 사용**
```js
var circle = require('./node.circle.js');
console.log( 'The area of a circle of radius 4 is '
           + circle.area(4));
```
아래는 실행방법과 실행 결과다.
```js
F:\BitNami\wampstack-5.4.22-0\apache2\htdocs\javascript\module>node node.demo.js
The area of a circle of radius 4 is 50.26548245743669
```

## 라이브러리
라이브러리는 모듈과 비슷한 개념이다. **모듈**이 프로그램을 구성하는 **작은 부품으로서의 로직**을 의미한다면 **라이브러리**는 자주 사용되는 로직을 재사용하기 편리하도록 **잘 정리한 일련의 코드들의 집합**을 의미한다고 할 수 있다. 프로그래밍의 세계에는 휼룡한 라이브러리가 많다. 좋은 라이브러리를 선택하고 잘 사용하는 것은 프로그래밍의 핵심이라고 할 수 있다. 

아래 예제는 유명 라이브러리인 jQuery를 사용하는 방법이다. 

jQuery 홈페이지에서 파일을 다운로드 받는다. 

http://jquery.com/

jQuery 메뉴얼을 이용해서 사용법을 파악한다.

http://api.jquery.com/

아래는 jQuery를 이용한 예제이다.

```js
<!DOCTYPE html>
<html>
<head>
    <script src="https://code.jquery.com/jquery-1.11.0.min.js"></script>
</head>
<body>
    <ul id="list">
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
    </ul>
    <input id="execute_btn" type="button" value="execute" />
    <script type="text/javascript">
     $('#execute_btn').click(function(){
        $('#list li').text('coding everybody');
     })
    </script>
</body>
</html>
```
다음은 jQuery를 이용하지 않고 동일한 기능을 구현한 예제이다.

```js
<!DOCTYPE html>
<html>
<body>
    <ul id="list">
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
        <li>empty</li>
    </ul>
    <input id="execute_btn" type="button" value="execute" />
    <script type="text/javascript">
    function addEvent(target, eventType,eventHandler, useCapture) {
        if (target.addEventListener) { // W3C DOM
            target.addEventListener(eventType,eventHandler,useCapture?useCapture:false);
        } else if (target.attachEvent) {  // IE DOM
            var r = target.attachEvent("on"+eventType, eventHandler);
        }
    }
    function clickHandler(event) {
        var nav = document.getElementById('list');
        for(var i = 0; i < nav.childNodes.length; i++) {
            var child = nav.childNodes[i];
            if(child.nodeType==3)
                continue;
            child.innerText = 'Coding everybody';
        }
    }
    addEvent(document.getElementById('execute_btn'), 'click', clickHandler);
    </script>
</body>
</html>
```

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/4705)