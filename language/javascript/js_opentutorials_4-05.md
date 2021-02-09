# 상속

## 상속(inheritance)이란?
객체는 연관된 로직들로 이루어진 작은 프로그램이라고 할 수 있다. 상속은 객체의 로직을 그대로 물려 받는 또 다른 객체를 만들 수 있는 기능을 의미한다. 단순히 물려받는 것이라면 의미가 없을 것이다. 기존의 로직을 수정하고 변경해서 파생된 새로운 객체를 만들 수 있게 해준다. 

아래 코드는 이전 시간에 살펴본 코드다.
```js
function Person(name){
    this.name = name;
    this.introduce = function(){
        return 'My name is '+this.name; 
    }   
}
var p1 = new Person('egoing');
document.write(p1.introduce()+"<br />");
```
결과
```js
My name is egoing
```
위의 코드를 아래와 같이 바꿔보자.
```js
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
var p1 = new Person('egoing');
document.write(p1.introduce()+"<br />");
```
결과는 같다. 하지만 상속을 위한 기본적인 준비를 마쳤다. 이제 상속을 해보자.

```js
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){
    this.name = name;
}
Programmer.prototype = new Person(); //상속, new Person()으로 객체를 생성. 
 
var p1 = new Programmer('egoing');
document.write(p1.introduce()+"<br />");
```
Programmer이라는 생성자를 만들었다. 그리고 이 생성자의 prototype과 Person의 객체를 연결했더니 Programmer 객체도 메소드 introduce를 사용할 수 있게 되었다. 

Programmer가 Person의 기능을 상속하고 있는 것이다. 단순히 똑같은 기능을 갖게 되는 것이라면 상속의 의의는 사라질 것이다. 부모의 기능을 계승 발전할 수 있는 것이 상속의 가치다.
```js
function Person(name){
    this.name = name;
}
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}
 
function Programmer(name){
    this.name = name;
}
Programmer.prototype = new Person();
Programmer.prototype.coding = function(){ //새로운 기능 추가
    return "hello world";
}
 
var p1 = new Programmer('egoing');
document.write(p1.introduce()+"<br />");
document.write(p1.coding()+"<br />");
```
결과
```js
My name is egoing
hello world
```
Programmer는 Person의 기능을 가지고 있으면서 Person이 가지고 있지 않은 기능인 메소드 coding을 가지고 있다. 

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/6572)