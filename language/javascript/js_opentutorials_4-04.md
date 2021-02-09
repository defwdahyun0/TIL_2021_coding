# this
this는 함수 내에서 **함수 호출 맥락(context)**를 의미한다. 맥락이라는 것은 상황에 따라서 달라진다는 의미인데 즉 함수를 어떻게 호출하느냐에 따라서 this가 가리키는 대상이 달라진다는 뜻이다. 함수와 객체의 관계가 느슨한 자바스크립트에서 this는 이 둘을 연결시켜주는 실질적인 연결점의 역할을 한다.

## 함수호출
함수를 호출했을 때 this는 무엇을 가르키는지 살펴보자. this는 전역객체인 window와 같다.
```js
function func(){
    if(window === this){
        document.write("window === this");
    }
}
func(); 
```
결과 
```js
window === this
```

## 메소드의 호출
객체의 소속인 메소드의 this는 그 객체를 가르킨다. 
```js
var o = {
    func : function(){
        if(o === this){ //this로 자기자신을 접근할 수 있다. func()는 window에 소속되어 있고, o.func()는 o에 속해있다.
            document.write("o === this");
        }
    }
}
o.func();   
```
결과
```js
o === this
```

## 생성자의 호출
아래 코드는 함수를 호출했을 때와 new를 이용해서 생성자를 호출했을 때의 차이를 보여준다.
```js
var funcThis = null; 
 
function Func(){
    funcThis = this;
}
var o1 = Func();
if(funcThis === window){
    document.write('window <br />');
}
 
var o2 = new Func();
if(funcThis === o2){ //if(o2==this)? o2는 undefined, false
    document.write('o2 <br />');
}
```
결과
```js
window 
o2
```
생성자는 빈 객체를 만든다. 그리고 이 객체내에서 this는 만들어진 객체를 가르킨다. 이것은 매우 중요한 사실이다. 생성자가 실행되기 전까지는 객체는 변수에도 할당될 수 없기 때문에 this가 아니면 객체에 대한 어떠한 작업을 할 수 없기 때문이다. 
```js
function Func(){
    document.write(o);
}
var o = new Func();
```
결과는 아래와 같다.
```js
undefined
```

## apply, call
```js
function sum(x,y){return x+y;} //sum이라는 함수 객체 //함수 literal
var sum2 = new Function('x','y','return x+y;');

var o = {} //객체 literal
var a = [1,2,3]; // new Array(1,2,3) 배열 literal

//literal 값을 만들 수 있게 해주는 문법적인 체계를 말한다.
```
함수의 메소드인 apply, call을 이용하면 this의 값을 제어할 수 있다. 
```js
var o = {}
var p = {}
function func(){
    switch(this){
        case o:
            document.write('o<br />');
            break;
        case p:
            document.write('p<br />');
            break;
        case window:
            document.write('window<br />');
            break;          
    }
}
func(); //window
func.apply(o); //o가 this
func.apply(p); //p가 this
```
결과
```js
window
o
p
```
객체는 주인(master), 메소드는 노예(slave).
js는 유연하다.
맥락상으로 함수가 종속되기도 한다.
함수의 어떤 소속인지가 객체.

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/6571)