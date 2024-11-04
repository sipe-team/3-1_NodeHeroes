# How To Create An NPM Package

해당 문서는 [totaltypescript.com](http://totaltypescript.com) 을 참고하여 작성되었으며,
핸즈온 형식의 포스팅을 기반으로 직접 npm package 를 배포하는 과정을 담았습니다.

<br/>

자세한 기술은 노션에 담았습니다.
여리 [링크](https://cord-teal-2f7.notion.site/How-To-Create-An-NPM-Package-12e02f7e0a15804ca5c7ff1d55fa5726?pvs=4)를 참조해주세요!

## 사용 기술

- 버전 제어용 Git
- TypeScript
- Prettier
- exports 를 위한 @arethetypeswrong/cli
- tsup
- Vitest
- Github Action
- Changesets

# 1. Git

## 1.1 repository 초기화

```jsx
git init
```

- 새로운 repo를 초기화 합니다.

## 1.2 .gitignore 설정

```jsx
node_modules;
```

- .gitignore 파일을 만들고 node_modules 를 파일 내 추가합니다.

## 1.3 Github repository 생성

- 레포지토리를 생성하고, 지금까지의 작업물을 commit 후 push 합니다.

# 2. package.json

## 2.1 package.json 파일 생성

[Semantic versioning](How%20To%20Create%20An%20NPM%20Package%2012e02f7e0a15804ca5c7ff1d55fa5726/Semantic%20versioning%2013102f7e0a1580fb8d82e9bab13ff6d7.md)

아래 값을 포함하는 pakcage.json 파일을 생성합니다.

```jsx
{
  "name": "fakify",
  "version": "1.0.0",
  "description": "가짜 데이터 생성용 npm package",
  "keywords": [
    "faker",
    "typescript"
  ],
  "homepage": "https://github.com/do-not-do-that/fakify",
  "bugs": {
    "url": "https://github.com/do-not-do-that/fakify/issues"
  },
  "author": "do-not-do-that",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/do-not-do-that/fakify.git"
  },
  "files": [
    "dist"
  ],
  "type": "module"
}

```

- name
  - 사람들에게 설치되는 패키지 이릠으로, npm 에서 고유해야합니다.
  - organization 범위를 만들수 있으며, 이를 통해서 고유하게 만들어질 수 있습니다.
- version
  - 패키지의 버전으로, semantic versioning 을 따라야합니다.
  - 새 버전을 게시할 때마다 이 숫자를 늘려야합니다.
- description & keywords
  - 패키지에 대한 짧은 설명으로, npm 레지스트리 검색 페이지에 노출됩니다.
- homepage
  - 패키지 홈페이지의 URL 입니다.
- bugs
  - 다른 사람들이 package에 대해 버그를 보고할 수 있는 URL 입니다.
- author
  - 제작자입니다.
  - 기여자가 여러 명인 경우 배열로 지정할 수 있습니다.
- repository
  - 패키지 저장소의 URL 입니다.
  - npm 레지스트리에서 GitHub 저장소로의 링크가 생성됩니다.
- files
  - 패키지를 설치할 때 포함되어야하는 파일의 배열입니다.
  - README.md, package.json, LICENSE 는 기본적으로 포함됩니다.
- type
  - 설정해둔 module 값은 우리의 패키지가 CommonJS 모듈이 아닌 ECMAScript 모듈을 사용한다는 것을 나타냅니다.

## 2.2 license 필드 추가

https://choosealicense.com/licenses/

```json
{
  "license": "MIT"
}
```

- 위 멘션되어있는 페이지에서 라이센스를 선택하여 package.json 내에 license 필드를 추가하세요.

### MIT 라이센스란?

[오픈소스 라이센스에 대한 지식](How%20To%20Create%20An%20NPM%20Package%2012e02f7e0a15804ca5c7ff1d55fa5726/%E1%84%8B%E1%85%A9%E1%84%91%E1%85%B3%E1%86%AB%E1%84%89%E1%85%A9%E1%84%89%E1%85%B3%20%E1%84%85%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%89%E1%85%A6%E1%86%AB%E1%84%89%E1%85%B3%E1%84%8B%E1%85%A6%20%E1%84%83%E1%85%A2%E1%84%92%E1%85%A1%E1%86%AB%20%E1%84%8C%E1%85%B5%E1%84%89%E1%85%B5%E1%86%A8%2013102f7e0a158065bc8ac77bf1a802b3.md)

## 2.3 LICENSE 파일 추가

```json
MIT License

Copyright (c) [year] [fullname]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

- 확장자 없이, LICENSE 파일을 위 내용과 같이 추가합니다.
- [year] 와 [fullname] 은 각각 현재 연도와 자신의 이름으로 변경합니다.

## 2.4 [README.md](http://README.md) 파일 추가

- [README.md](http://README.md) 패키지에 대한 설명이 있는 파일을 만듭니다.

# 3. TypeScript

## 3.1 TypeScript 설치

```json
npm install --save-dev typescript
```

- —save-dev 플래그를 넣었기 때문에, 다른 사람들이 저의 패키지를 설치할 때는 포함되지 않습니다.

## 3.2 tsconfig.json 설정

```json
{
  "compilerOptions": {
    /* Base Options: */
    "esModuleInterop": true,
    "skipLibCheck": true,
    "target": "es2022",
    "allowJs": true,
    "resolveJsonModule": true,
    "moduleDetection": "force",
    "isolatedModules": true,
    "verbatimModuleSyntax": true,

    /* Strictness */
    "strict": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitOverride": true,

    /* If transpiling with TypeScript: */
    "module": "NodeNext",
    "outDir": "dist",
    "rootDir": "src",
    "sourceMap": true,

    /* AND if you're building for a library: */
    "declaration": true,

    /* AND if you're building for a library in a monorepo: */
    "declarationMap": true
  }
}
```

## 3.3 DOM에 대한 구성

```json
{
  "compilerOptions": {
    // ...other options
    "lib": ["es2022"]
  }
}
```

- 만약 코드가 DOM에서 실행되는게 아니라면, 위 컴파일러 옵션도 추가합니다.

## 3.4 소스 파일 생성

## 3.5 인덱스 파일 생성

```json
export { getRandomKoreanName } from "./fakify.js";
```

- 여기서 js 는 조금 이상하게 보일 수 있습니다.
- 왜 .js 일까요?

https://www.totaltypescript.com/relative-import-paths-need-explicit-file-extensions-in-ecmascript-imports

## 3.6 build 스크립트 작성

```json
{
  "scripts": {
    "build": "tsc"
  }
}
```

- 위의 설정으로 TypeScript 가 JavaScript 로 컴파일 됩니다.

## 3.7 빌드 실행

```json
npm run build
```

- 위 명령어로 빌드하게 되면, 컴파일된 자바스크립트 코드가 담긴 dist 폴더가 생성됩니다.

## 3.8 .gitignore 에 dist 추가

## 3.9 ci script 설정

```json
{
  "scripts": {
    "ci": "npm run build"
  }
}
```

- ci 스크립트를 추가합니다.

# 4. Prettier

## 4.1 prettier 설치

```json
npm install --save-dev prettier
```

## 4.2 .prettierrc 설정

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 80,
  "tabWidth": 2
}
```

- 자세한 옵션 목록은 아래 링크에서 확인할 수 있습니다.
- https://prettier.io/docs/en/options.html

## 4.3 format 스크립트 설정

```json
{
  "scripts": {
    "format": "prettier --write ."
  }
}
```

## 4.4 format 스크립트 실행

```json
npm run format
```

## 4.5 check-format 스크립트 설정

```json
{
  "scripts": {
    "check-format": "prettier --check ."
  }
}
```

- 위 스크립트를 이용해 프로젝트 내 모든 파일이 올바른 포맷을 가졌는지 확인할 수 있습니다.

## 4.6 CI 스크립트에 추가하기

```json
{
  "scripts": {
    "ci": "npm run build && npm run check-format"
  }
}
```

# 5. export 와 main, @arethetypeswrong/cli 설정

https://www.npmjs.com/package/@arethetypeswrong/cli

@arethetypeswrong/cli 는, npm 패키지 내용을 분석하여 TypeScript 나 ESM 관련 모듈 버그를 파악하는 도구입니다.

## 5.1 **@arethetypeswrong/cli 설치**

```json
npm install --save-dev @arethetypeswrong/cli
```

## 5.2 check-exports 스크립트 설정

```json
{
  "scripts": {
    "check-exports": "attw --pack ."
  }
}
```

- 위 스크립트로 패키지의 exports 가 올바른지 확인할 수 있습니다.

## 5.3 check-exports 스크립트 실행

```json
npm run check-exports
```

- 강렬한 리스트를 볼 수 있는데, 위는 어떤 버전의 Node 나 bundler 도 우리 패키지를 사용할 수 없다는 것을 의미합니다.

## 5.4 main 설정

```json
{
  "main": "dist/index.js"
}
```

- package.json 파일 내 main 필드를 추가합니다.
- Node에게 패키지의 진입점을 알려주어요 🙂

## 5.5 다시 check-exports 실행

```json
npm run check-exports
```

- 하나의 경고가 있는데, 해당 이슈는 우리가 만든 패키지가 ESM 을 사용하는 시스템과 호환된다는 것을 알려줍니다.
- 만약 CJS를 사용한다면, dynamic import 를 이용해서 가져와야한다는 의미입니다.

## 5.6 CJS 경고 수정

```json
{
  "scripts": {
    "check-exports": "attw --pack . --ignore-rules=cjs-resolves-to-esm"
  }
}
```

- 만약 CJS를 지원하지 않으려면 위와 같이 스크립트를 변경하세요.
- 다시 실행하면, 전부 녹색으로 변합니다!

## 5.7 CI 스크립트에 추가하기

```json
{
  "scripts": {
    "ci": "npm run build && npm run check-format && npm run check-exports"
  }
}
```

- check-exports 를 ci 스크립트에 추가합니다.

# 6. tsup 을 이용한 듀얼 퍼블리싱(CJS, ESM 동시 지원)

[Dual Package Hazard 란?](How%20To%20Create%20An%20NPM%20Package%2012e02f7e0a15804ca5c7ff1d55fa5726/Dual%20Package%20Hazard%20%E1%84%85%E1%85%A1%E1%86%AB%2013002f7e0a1580fbba58ee50f6b32196.md)

<aside>
💡

만약 ES Modules 형식만 지원하고 싶다면, 이 단계는 건너뛰세요.
원 저자 또한 이 단계를 피하는게 좋다고 조언합니다.

</aside>

## 6.1 tsup 설치

```json
npm install --save-dev tsup
```

tsup 은 esbuild를 기반으로 만들어진 도구로, TypeScript 코드를 두 가지 형식으로 컴파일 해줍니다.

## 6.2 tsup.config.ts 파일 생성

```json
import { defineConfig } from "tsup";

export default defineConfig({
  entryPoints: ["src/index.ts"],
  format: ["cjs", "esm"],
  dts: true,
  outDir: "dist",
  clean: true,
});
```

- entryPoints
  - 패키지의 진입점을 나타냅니다.
- format
  - 출력할 형식의 배열입니다.
  - cjs(CommonJS)와 esm을 사용하고 있습니다.
- dts
  - tsup 선언 파일을 생성하도록 알려주는 부울 값입니다.
- outDir
  - 컴파일된 코드의 출력 디렉토리 입니다.
- clean
  - 빌드하기 전 출력 디렉토리를 정리하라고 알려줍니다.

## 6.3 build 스크립트 변경

```json
{
  "scripts": {
    "build": "tsup"
  }
}
```

- tsc 대신 tsup 을 이용합니다.

## 6.4 exports 필드 추가

```json
{
  "exports": {
    "./package.json": "./package.json",
    ".": {
      "import": "./dist/index.js",
      "default": "./dist/index.cjs"
    }
  }
}
```

- `exports` 필드는 패키지를 사용하는 프로그램에 패키지의 CJS 및 ESM 버전을 찾는 방법을 알려줍니다.
- 우리의 경우, `import` 구문을 사용할 경우 `dist/index.js` 파일을, `require` 구문을 사용할 경우 `dist/index.cjs` 파일을 사용하도록 경로를 지정하고 있습니다.
- 또한 `./package.json` 파일에 쉽게 접근할 수 있도록 `exports` 필드에 `./package.json` 경로를 추가하여 특정 도구들이 package.json 파일에 쉽게 접근할 수 있도록 합니다.

## 6.5 빌드 하고, check-export 다시 한번 더!

```json
npm run build
npm run check-exports
```

## 6.6 TypeScript 를 linter로 전환

우리는 더이상 코드를 컴파일 하기 위해 tsc 를 사용하지 않고,

tsup은 실제 코드의 오류를 확인하는 것이 아닌 JavaScript로 변환만 해주기 때문에

ci 코드에 TypeScript 오류가 있어도 스크립트에서 오류가 발생하지 않습니다.

고쳐봅시다!

### 6.6.1 tsconfig.json 에 noEmit 속성 추가

```json
{
  "compilerOptions": {
    // ...other options
    "noEmit": true
  }
}
```

### 6.6.2 tsconfig.json 에 사용하지 않은 필드 제거

- outDir
- rootDir
- sourceMap
- declaration
- declarationMap

새로운 린팅 설정에서는 필요하지 않기 때문에, 없애줍니다.

### 6.6.3 module 속성 Preserve 로 변경

```json
{
  "compilerOptions": {
    // ...other options
    "module": "Preserve"
  }
}
```

- 선택적으로 module 속성을 Preserve 로 변경할 수 있습니다.
- 이 설정을 하면, 확장자를 가진 파일을 가져올 필요 없습니다.

```json
export * from "./utils";
```

이렇게 할 수 있어요!

### 6.6.4 lint 스크립트 추가

```json
{
  "scripts": {
    "lint": "tsc"
  }
}
```

- lint 스크립트를 추가합니다.

### 6.6.5 lint 스크립트 ci 에 추가

```json
{
  "scripts": {
    "ci": "npm run build && npm run check-format && npm run check-exports && npm run lint"
  }
}
```

- 이렇게 하면, CI 프로세스의 일부로 TypeScript 오류가 발생합니다.

# 7. Vitest 로 테스트하기

## 7.1 vitest 설치

```json
npm install --save-dev vitest
```

- jest 와 비슷하지만.. ESM과 TypeScript를 위한 최신 버전 테스트 러너입니다! 설치설치설치설치

## 7.2 테스트 생성

`src/파일명.test.ts` 로 테스트를 생성합니다.

- code

  ```json
  import { describe, it, expect } from 'vitest';
  import { getRandomKoreanName } from './fakify.js';

  // 성과 이름 배열
  const lastNames = [
    '김',
    '이',
    '박',
    '최',
    '정',
    '강',
    '조',
    '윤',
    '장',
    '임',
    '홍',
  ];
  const firstNames = [
    '민준',
    '서준',
    '도윤',
    '예준',
    '시우',
    '하준',
    '주원',
    '지호',
    '지훈',
    '준우',
    '예서',
    '서윤',
    '서연',
    '지우',
    '하은',
    '민서',
    '수아',
    '하윤',
    '다은',
    '예린',
    '은비',
  ];

  describe('getRandomKoreanName', () => {
    it('should return a string', () => {
      const name = getRandomKoreanName();
      expect(typeof name).toBe('string');
    });

    it('should return a name with a valid last name and first name', () => {
      const name = getRandomKoreanName();
      const lastName = name[0]; // 성은 이름의 첫 글자로 가정
      const firstName = name.slice(1); // 나머지는 이름으로 간주

      // 올바른 성과 이름인지 확인
      expect(lastNames).toContain(lastName);
      expect(firstNames).toContain(firstName);
    });

    it('should return different names on multiple calls', () => {
      const name1 = getRandomKoreanName();
      const name2 = getRandomKoreanName();

      // 여러 번 호출했을 때, 이름이 다를 가능성이 있음을 확인
      expect(name1).not.toBe(name2);
    });
  });

  ```

## 7.3 test 스크립트 설정

```json
{
  "scripts": {
    "test": "vitest run"
  }
}
```

## 7.4 test 스크립트 실행

```json
npm run test
```

## 7.5 dev 스크립트 설정

```json
{
  "scripts": {
    "dev": "vitest"
  }
}
```

- 일반적으로는 개발하는 동안 watch 모드에서 테스트를 실행하게 됩니다.
- 위 스크립트를 추가하세요.

## 7.6 CI 스크립트에 추가하기

```json
{
  "scripts": {
    "ci": "npm run build && npm run check-format && npm run check-exports && npm run lint && npm run test"
  }
}
```

## 8. GitHub Actions 로 CI 설정하기

이번 단계는 패키지가 항상 working 상태를 유지하도록 하는데에 중요한 단계입니다.

## 8.1 워크플로 생성

```json
name: CI

on:
  pull_request:
  push:
    branches:
      - main

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  ci:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Use Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20"

      - name: Install dependencies
        run: npm install

      - name: Run CI
        run: npm run ci
```

- `.github/workflows/ci.yml` 파일을 만드세요.

- name
  - 워크플로우의 이름입니다.
- on
  - 이 워크플로우가 실행되어야하는 시점을 정의합니다.
  - PR 시점과 main 브랜치에 push 되었을 때를 의미합니다.
- concurrency
  - 기존 실행을 취소하여 워크블로우의 여러 인스턴스가 동시에 실행되는 것을 방지합니다.
- jobs
  - 실행할 작업 세트입니다.
  - 우리의 경우, ci 라는 작업이 하나 있습니다.
- actions/checkout@v4
  - 저장소에서 코드를 체크아웃 합니다.
- actions/setup-node@v4
  - NODE.JS 와 npm을 설정합니다.
- npm install
  - 프로젝트의 종속성을 설치합니다.
- npm run ci
  - 프로젝트의 CI 스크립트를 실행합니다.

만약 CI 프로세스의 어떤 부분이든 실패하면 워크플로우가 실패하고, Github는 커밋 옆에 X 표시로 알려줍니다.

## 8.2 워크플로우 테스트

- Github에 변경사항을 푸시하고 리포지토리에서 Actions 탭을 확인하세요.
- 워크 플로우가 실행되는 것을 볼 수 있습니다.

# 9. Changesets로 Publish 하기

- Changesets는 패키지를 버전화하고 게시하는데 도움이 되는 도구입니다.
- npm 에 패키지를 게시하는 모든 사람들에게 추천한다고 하네요!

## 9.1 @changesets/cli 설치

```json
npm install --save-dev @changesets/cli
```

## 9.2 Changesets 초기화

```json
npx changeset init
```

- 위 명령어를 실행하면 .changeset 폴더가 생성됩니다.
- .changeset 폴더 내에는 config.json 파일이 존재합니다.

## 9.3 changeset 릴리즈 공개 설정

```json
// .changeset/config.json
{
  "access": "public"
}
```

- access 를 public으로 설정하지 않으면 패키지가 npm에 게시되지 않습니다.

## 9.4 commit 설정

```json
// .changeset/config.json
{
  "commit": true
}
```

- 이 설정을 추가하면, 버전 관리가 끝난 후 변경 사항이 저장소에 커밋됩니다.

## 9.5 local-release 스크립트 설정

```json
{
  "scripts": {
    "local-release": "changeset version && changeset publish"
  }
}
```

- CI 프로세스 실행 이후 패키지를 npm에 게시합니다.
- 로컬 머신에서 패키지의 새로운 버전을 릴리즈하려고 할 때 실행하는 명령입니다.

## 9.6 prepublishOnly

```json
{
  "scripts": {
    "prepublishOnly": "npm run ci"
  }
}
```

- 이렇게 하면 npm에 패키지를 게시하기 전에 자동으로 CI 프로세스가 실행됩니다.

## 9.7 changeset 추가

```json
npx changeset
```

## 9.8 변경사항 커밋

```json
git add .
git commit -m "Prepare for initial release"
```

## 9.9 local-release 스크립트 실행

```json
npm run local-release
```

- 이렇게 하면 CI 프로세스가 실행되고, 패키지의 버전이 관리되고, npm에 게시됩니다.
- 패키지의 레포지토리에 [CHANGELOG.md](http://CHANGELOG.md) 라는 릴리즈 변경사항을 자세히 설명하는 파일이 생성됩니다.
- 이는 릴리즈 할 때마다 업데이트 됩니다.

# 대망의 10! 그래서 진짜 개발-배포 프로세스는요?

## 10.1 코드 변경

- 하나의 커밋 혹은 여러 개의 커밋 후 새로운 버전을 릴리즈하려면 다음 단계로 넘어갑니다.

## 10.2 changeset 생성

```json
npx changeset
```

- 위 명령어를 이용하여 changeset을 생성합니다.
- 명령어를 실행하면 SemVer 스펙을 따르는 변경 타입을 선택할 수 있고, Summary 를 작성하게 됩니다.
- .changeset/{랜덤한 파일 이름}.md 이 생깁니다.
- 이 명령어를 실행했다고 해서 곧바로 [CHANGELOG.md](http://CHANGELOG.md) 가 변하거나, package.json 의 패키지 버전이 올라가진 않습니다.

## 10.3 repository PUSH

커밋된 내용을 pr 이나 push 하여 패키지에 이상이 없는지 확인하세요.

push 이후 github action 을 통해 test, lint 등의 작업들이 자동으로 이루어집니다.

## 10.4 패키지 배포

- 패키지를 배포할 때가 된 것 같나요?

```json
npm run local-release
```

- npm 에 로그인되어있는 로컬에서 위 명령어를 입력하면 npm 레지스트리에 배포됩니다.
- 위 명령어를 입력하여 npm 레지스트리에 배포하세요.
- 배포와 더불어서 자동으로 커밋(changesets 가 해준 커밋)이 생성됩니다.
- 깃헙 레포에 push 하면, changelog 와 package 버전이 변경됩니다!
