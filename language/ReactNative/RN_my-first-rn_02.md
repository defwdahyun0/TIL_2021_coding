# 2장 리액트 네이티브 시작하기

## 2.1 개발 환경 준비하기

### 2.1.1 왓치맨 설치
brew install watchman

### 2.1.2 Node.js 설치
nvm 이용 권장

```js
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

.zshrc 파일 수정 (vi .zshrc)
```js
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" 
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

```js
nvm --version
nvm install --lts
node --version
```

### 2.1.3 파이썬 설치
파이썬 2버전 설치, 맥에서는 따로 설치할 필요 없다.

### 2.1.4 iOS 개발 환경
* Xcode 설치
* 코코아팟 설치
sudo gem install cocoapods
* 시뮬레이터

### 2.1.5 JDK 설치
brew cask install adoptopenjdk/openjdk/adoptopenjdk8 (x)
brew install --cask adoptopenjdk/openjdk/adoptopenjdk8 (o)

### 2.1.6 안드로이드 스튜디오 설치
* https://bit.ly/android-ide-download 설치 및 환경설정

.zshrc 파일을 열고 다음 내용 추가
```js
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```
설치 확인
```js
adb --version
```

### 2.1.7 에디터 설치
vscode

## 2.2 리액트 네이티브 프로젝트

### 2.2.1 Expo
* Expo : https://expo.io
회원가입 후 프로젝트 실행

```js
npm install --global expo-cli
expo init my-first-expo
cd my-first-expo
npm start
```

### 2.2.2 리액트 네이티브 CLI
```js
npx react-native init MyFirstCLI
cd MyFirstCLI
npm run ios
npm run android
```

### 2.2.3 메인 파일 변경
