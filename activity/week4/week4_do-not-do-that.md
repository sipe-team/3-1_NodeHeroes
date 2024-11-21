# 🐸 `frogsay` 프로젝트 개발 첫 시작

### 시작하며

`frogsay`는 슬픈 개구리 페페의 ASCII 아트를 통해 메시지를 출력하는 Npm 패키지를 목표로 한다!

기존의 `cowsay`에서 영감을 얻어 슬픈 개구리 페페가 말하는 패키지를 개발할 것!

---

### 프로젝트 구조 설계

`frogsay`의 초기 개발 단계에서 고려한 프로젝트 구조는 다음과 같다:

#### 1. **패키지 기본 구조**

- `index.js`: 패키지의 진입점. 메시지를 받아 ASCII 아트를 생성하는 함수들을 포함.
- `src/`: 개구리 아트를 정의하고 텍스트를 처리하는 유틸리티 함수 모음.
  - `art.js`: 개구리 ASCII 아트를 정의.
  - `textFormatter.js`: 텍스트를 말풍선 형태로 변환하는 함수.
- `bin/`: CLI(Command Line Interface) 실행 스크립트.
  - `frogsay.js`: 명령어로 실행할 때의 로직을 처리.

#### 2. **Npm CLI 지원**

CLI 명령어를 통해 `frogsay`를 실행할 수 있도록 설계한다. 이를 위해 다음을 고려:

- `package.json`에 `bin` 속성을 추가.
- 사용자 입력을 받아 CLI 환경에서 ASCII 아트를 출력.

---

### 새롭게 공부한 패키지들

`frogsay`를 개발하며 새롭게 공부하거나 다시 익힌 패키지는 다음과 같다:

#### 1. [commander.js](https://www.npmjs.com/package/commander)

CLI 애플리케이션의 명령어와 옵션을 쉽게 관리할 수 있는 패키지.

- 사용자 입력을 파싱하고 다양한 플래그나 옵션을 추가하기 위해 사용.
- `frogsay` CLI에서 메시지를 입력받는 데 활용.

#### 2. [chalk](https://www.npmjs.com/package/chalk)

터미널 텍스트 스타일링을 위한 라이브러리.

- 메시지와 개구리 ASCII 아트를 색깔 있게 출력하기 위해 고려 중.

#### 4. [boxen](https://www.npmjs.com/package/boxen)

문자열을 박스 형태로 꾸며주는 패키지.

- `frogsay`에서 개구리 말풍선 스타일을 꾸미는 데 참고!
