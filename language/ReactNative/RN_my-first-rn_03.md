# 3장 컴포넌트

```js
expo init react-native-component
```

## 3.1 JSX
### 3.1.1 하나의 부모
하나의 부모로 나머지 요소를 감싸서 반환해야 한다.
(부모) 컴포넌트 예시 : <view> , <fragment>=<>

### 3.1.2 자바스크립트 변수

### 3.1.3 자바스크립트 조건문
* if
* 삼항 연산자 {name === a ? a : b}
* AND && OR !

### 3.1.4 null과 undefined
jsx는 null은 허용하지만 undefined는 오류가 발생한다.

### 3.1.5 주석
{/* */}

### 3.1.6 스타일링
인라인 스타일링을 우선 살펴본다.
style에 문자열로 입력하는 것이 아니라 객체 형태로 입력해야 한다.
- 연결된 이름은 카멜표기법으로 표시한다. ex ReactNative

<View
    style = {{ }}
>

## 3.2 컴포넌트
재사용이 가능한 조립블록

### 3.2.1 내장 컴포넌트

* 리액트 네이티브 컴포넌트 : https://reactnative.dev/docs/components-and-apis
* Button 컴포넌트 : https://reactnative.dev/docs/button

### 3.2.2 커스텀 컴포넌트 만들기
MyButton.js
```js
import React from 'react';
import { TouchableOpacity, Text } from 'react-native';

const MyButton = () => {
    return (
        <TouchableOpacity>
            <Text style={{fontSize:24}}>MyButton</Text>
        </TouchableOpacity>
    );
};

export default MyButton;
```

App.js
```js
import React from 'react';
import { Text,View } from 'react-native';
import MyButton from './components/MyButton';

const App = () => {
    return (
    <View
        style={{

        }}
    >
        <Text
            style={{

            }}
        >
        My Button Component
        </Text>
        <MyButton />
    </View>
    );
};

export default App;
```

이후 클릭에 대한 속성 지정

MyButton.js
```js
import React from 'react';
import { TouchableOpacity, Text } from 'react-native';

const MyButton = () => {
    return (
        <TouchableOpacity
            style={{

            }}
            onPress={() => alert('Click!!!')}
        >
            <Text style={{}}>My Button</Text>
        </TouchableOpacity>
    );
};

export default MyButton;
```

## 3.3 props와 state
다양한 기능과 역할

### 3.3.1 props
properties, 부모 컴포넌트로부터 전달된 속성값 혹은 상속받은 속성값
부모가 자식 props 설정하면 변경이 불가능

* props 전달과 사용
```js
...
const App = () => {
    return (
        <MyButton title="Button">Children Props</MyButton>
    );
};
...
```
```js
...
const MyButton = props => {
    return (
    );
};
...
```

* defaultProps : 기본
* propTypes
npm install prop-types
```js
MyButton.propTypes = {
    title: Proptypes.string,
    {/*title: Proptypes.string.isRequired,*/}{/*필수전달여부*/}
};
```
```js
const MyButton = props => {
    return (
        <TouchableOpacity
            onPress={()=>props.onPress()}
        >
    );
};
MyButton.propTypes = {
    title: Proptypes.string.isRequired,
    onPress: Proptypes.func.isRequired,{/*함수필수전달여부*/})
};
```

### 3.3.2 state
state는 컴포넌트 내부에서 생성되고 값을 변경할 수 있으며 

