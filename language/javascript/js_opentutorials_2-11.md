# 객체

## 객체(Object)
새창으로 열기
지금까지 살펴본 배열은 아이템에 대한 식별자로 숫자를 사용했다. 데이터가 추가되면 배열 전체에서 중복되지 않는 인덱스가 자동으로 만들어져서 추가된 데이터에 대한 식별자가 된다. 이 인덱스를 이용해서 데이터를 가져오게 되는 것이다. 만약 인덱스로 문자를 사용하고 싶다면 객체(dictionary)를 사용해야 한다. 다른 언어에서는 연관배열(associative array) 또는 맵(map), 딕셔너리(Dictionary)라는 데이터 타입이 객체에 해당한다.

## 객체의 생성
다음은 객체를 만드는 법이다.

```js
var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
```
위의 예제에서 egoing은 key가 되고, 10은 value가 된다. 아래는 객체를 만드는 다른 방법이다.

```js
var grades = {};
grades['egoing'] = 10;
grades['k8805'] = 6;
grades['sorialgi'] = 80;
```
아래와 같은 방법으로 객체를 만들수도 있다.

```js
var grades = new Object();
grades['egoing'] = 10;
grades['k8805'] = 6;
grades['sorialgi'] = 80;
```
객체를 만들었으니 이제는 객체에서 필요한 값을 가져와보자. 다음은 sorialgi라는 이름(key)으로 저장된 값을 가져오는 법이다. 결과는 80이다.
```js
var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
alert(grades['sorialgi']);
```
다음 방법으로도 객체의 속성에 접근 할 수 있다.
```js
alert(grades.sorialgi);
```
다음은 객체에 저장된 데이터를 기준으로 반복작업을 하는 방법이다.

```js
var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
for(key in grades) {
    document.write("key : "+key+" value : "+grades[key]+"<br />");
}
```
결과는 아래와 같다.

```js
key :   egoing value : 10
key :   k8805 value : 6
key :   sorialgi value : 80
```
**배열은 순서가 있고, 객체는 순서가 없다.**

for 문은 in 뒤에 따라오는 배열의 key 값을 in 앞의 변수 name에 담아서 반복문을 실행한다. 반복문이 실행될 때 변수 key의 값으로 egoing, k8805, sorialgi가 순차적으로 할당되기 때문에 grades[key]를 통해서 객체의 값을 알아낼 수 있다.

객체에는 객체를 담을수도 있고, 함수도 담을 수 있다. 

```js
var grades = {
    'list': {'egoing': 10, 'k8805': 6, 'sorialgi': 80},
    'show' : function(){
        //console.log(this.list); //this는 현재 객체를 의미함
        for(var name in this.list){
            document.write(name+':'+this.list[name]+"<br />");
        }
    }
};
grades.show();
```
이것은 자바스크립트를 이용한 객체 지향 프로그래밍 기법의 핵심이 되는 성질로 취지에 따라서 로직을 객체에 그룹핑해서 객체라는 부품을 조립해서 소프트웨어라는 완제품을 만들 수 있게 해준다. 객체 지향에 대해서는 뒤에서 자세히 살펴본다.

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/6491)