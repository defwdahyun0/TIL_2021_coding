# 배열

## 배열
배열(array)이란 연관된 데이터를 모아서 통으로 관리하기 위해서 사용하는 데이터 타입이다. 변수가 하나의 데이터를 저장하기 위한 것이라면 배열은 여러 개의 데이터를 하나의 변수에 저장하기 위한 것이라고 할 수 있다. 아래의 예제를 보자. 변수 name에는 문자 egoing이 할당되었다. 이제부터 name을 호출하면 문자 egoing을 사용할 수 있다.

```js
var name = 'egoing'
alert(name);
```

## 배열의 생성
그렇다면 여러 개의 데이터를 하나의 변수에 담아서 관리할 수 있는 방법은 없을까? 있다. 배열을 쓰면 된다. 변수 member에 회원정보를 담아보자. 대괄호([])는 배열을 만드는 기호다. 대괄호 안에 데이터를 콤마(,)로 구분해서 나열하면 배열이 된다.

```js
var member = ['egoing', 'k8805', 'sorialgi']
```
하나의 변수에 3개의 데이터를 담았다. 각각의 데이터를 원소(Element)이라고 부른다. 자 그럼 이 데이터를 꺼내오려면 어떻게 해야 할까? 아래의 예제를 보자.

```js
var member = ['egoing', 'k8805', 'sorialgi']
alert(member[0]);
alert(member[1]);
alert(member[2]);
```
결과는 아래의 문자열을 차례로 경고창으로 출력 할 것이다.
```js
egoing
k8805
sorialgi
```
즉 배열에 담겨있는 값을 가져올 때는 대괄호 안에 숫자를 넣는다. 이 숫자를 색인(index)라고 부르고 0부터 시작한다. 즉 첫번째 원소(egoing)를 가져오려면 대괄호 안에 0을 넣어주어야 한다는 것이다. 두번째는 1, 세번째는 2를 입력한다. 이 값을 이용해서 배열에 저정된 값을 가져올 수 있다.

## 배열이 없다면
새창으로 열기
그렇다면 배열이 없다면 어떻게 될까? 예를 들어 맴버의 이름을 제공하는 함수를 제공해야 한다고 해보자. 그런데 함수는 하나의 값만을 반환(return) 할 수 있다. 아래의 예를 보자.

```js
function get_member1(){
    return 'egoing';
}
document.write(get_member1());
 
function get_member2(){
    return 'k8805';
}
document.write(get_member2());
 
 
function get_member3(){
    return 'sorialgi'
}
document.write(get_member3());
```
하나의 함수는 하나의 값만을 반환할 수 있기 때문에 위와 같이 각각의 회원정보를 반환하는 함수를 만들었다.

이번엔 배열를 이용한 아래의 코드를 보자. 맴버를 담고 있는 배열를 반환하고 있다. 간단하지 않은가?

```js
function get_members(){
    return ['egoing', 'k8805', 'sorialgi'];
}
var members = get_members();
document.write(members[0]);
document.write(members[1]);
document.write(members[2]);
```

## 배열의 사용
배열의 진가는 반복문과 결합했을 때 나타난다. 반복문으로 리스트에 담긴 정보를 하나씩 꺼내서 처리 할 수 있기 때문이다. 다음 예제를 보자

```js
function get_members(){
    return ['egoing', 'k8805', 'sorialgi'];
}
members = get_members();
// members.length는 배열에 담긴 값의 숫자를 알려준다. 
for(i = 0; i < members.length; i++){
    // members[i].toUpperCase()는 members[i]에 담긴 문자를 대문자로 변환해준다.
    document.write(members[i].toUpperCase());   
    document.write('<br />');
}
```
결과는 아래와 같다.
```js
egoing
k8805
sorialgi
```
위의 예제에서 주목해야 할 것은 반복문과 배열을 결합한 부분이다. 반복문을 이용해서 배열 members의 내용을 하나씩 꺼낸 후에 이름의 첫글자를 대문자로 변경한 후에 출력하고 있다. 정리하면, 배열이란 연관된 정보를 하나의 그룹으로 관리하기 위해서 사용한다. 그리고 그 정보를 처리 할 때는 반복문을 이용한다.

## 배열의 제어
배열은 복수의 데이터를 효율적으로 관리, 전달하기 위한 목적으로 고안된 데이터 타입이다. 따라서 데이터의 추가/수정/삭제와 같은 일을 편리하게 할 수 있도록 돕는 다양한 기능을 가지고 있다. 몇가지 중요한 기능들만 살펴보자.

### 배열의 크기
아래와 같은 방법으로 배열의 크기를 알아낼 수 있다. 결과는 5이다.

```js
var arr = [1, 2, 3, 4, 5];
alert(arr.length);
```

## 배열의 조작
### 추가
다음은 배열의 끝에 원소를 추가하는 방법이다. [push](https://opentutorials.org/course/50/105)는 인자로 전달된 값을 배열(li)에 추가하는 명령이다. 배열 li의 값은 a, b, c, d, e, f가 됐다.
```js
var li = ['a', 'b', 'c', 'd', 'e'];
li.push('f');
alert(li);
```
다음은 복수의 원소를 배열에 추가하는 방법이다. [concat](https://opentutorials.org/course/50/102)은 인자로 전달된 값을 추가하는 명령이다.
```js
var li = ['a', 'b', 'c', 'd', 'e'];
li = li.concat(['f', 'g']);
alert(li);
```
다음은 배열의 시작점에 원소를 추가하는 방법이다. 배열 li는 z, a, b, c, d, e가 됐다. [unshift](https://opentutorials.org/course/50/112)는 인자로 전달한 값을 배열의 첫번째 원소로 추가하고 배열의 기존 값들의 색인을 1씩 증가시킨다.
```js
var li = ['a', 'b', 'c', 'd', 'e'];
li.unshift('z');
alert(li);
```
만약 두번째 인덱스 뒤에 대문자 B를 넣고 싶다면 아래와 같이한다. [splice](https://opentutorials.org/course/50/110)는 첫번째 인자에 해당하는 원소부터 두번째 인자에 해당하는 원소의 숫자만큼의 값을 배열로부터 제거한 후에 리턴한다. 그리고 세번째 인자부터 전달된 인자들을 첫번째 인자의 원소 뒤에 추가한다.
```js
var li = ['a', 'b', 'c', 'd', 'e'];
li.splice(2, 0, 'B');
alert(li);
```

## 제거
다음은 배열의 첫번째 원소를 제거하는 방법이다. [shift](https://opentutorials.org/course/50/107)를 사용하면 된다. 아래 결과는 b, c, d, e 다.
```js
var li = ['a', 'b', 'c', 'd', 'e'];
li.shift();
alert(li);
```
다음은 배열 끝점의 원소를 배열 li에서 제거한다. 이때는 [pop](https://opentutorials.org/course/50/104)를 사용한다. 결과는 a, b, c, d 다.
```js
var li = ['a', 'b', 'c', 'd', 'e'];
li.pop();
alert(li);
```
## 정렬
다음은 정렬하는 방법이다. 결과는 a, b, c, d, e 다.
```js
var li = ['c', 'e', 'a', 'b', 'd'];
li.sort();
alert(li);
```
역순으로 정렬하고 싶을 때는 아래와 같이 한다.

```js
var li = ['c', 'e', 'a', 'b', 'd'];
li.reverse();
alert(li);
```

## Reference
* [생활코딩 javascript](https://opentutorials.org/course/743/4736)