# 9장

## 9.1 준비
```js
expo init react-native-keyword
```
### 9.1.1 내비게이션
```js
cd react-native-keyword
npm install @react-navigation/native
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
npm install @react-navigation/stack @react-navigation/bottom-tabs
```

### 9.1.2 라이브러리
```js
npm install styled-components prop-types
```

### 9.1.3 프로젝트 파일 구조

## 9.2 파이어베이스

* https://console.firebase.google.com/

### 9.2.2 데이터베이스
* https://bit.ly/location-firebase
위치 지정은 나중에 하기

### 9.2.3 스토리지
서버 코드 없이 사용자의 사진 동영상 등 저장 -> 필요 x

## 9.3 앱 아이콘과 로딩 화면
아이콘 1024x1024 icon.png
로딩 1242x2436 splash.png

미리 불러오기
* 이미지 cacheImages
* 폰트 cacheFonts
이를 이용해 _loadAssets 함수 구성
이미지나 폰트 미리 불러오면 느리게 적용되는 문제 개선

미리 불러와야하는 항목 불러오고 화면 렌더링되도록 AppLoading 컴포넌트의 startAsync에 _loadAssets 함수 지정. 완료되었을 때 isReady 상태를 변경

로딩화면 배경색 화면 이미지의 배경색과 동일하도록