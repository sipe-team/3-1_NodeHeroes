# 1week note

<aside>
💡

1주차 미션 : npm 배포 프로세스 경험해보기

</aside>

### 무엇을 했나?

[https://www.totaltypescript.com/how-to-create-an-npm-package](https://www.totaltypescript.com/how-to-create-an-npm-package)

→ 요 가이드 보고 demo-package를 npm 에 배포 해봄

패키지를 npm 에 올려보는 것을 처음 해봄! 

이런 프로세스를 진행함

- npm 계정 생성
- 레포 생성
- 프로젝트 Init
- package.json 설정
- 타입스크립트 설정
- 패키징을 위한 tool 설치 (`@arethetypesworng` , `@tsup`)
- 테스트코드 작성
- actions workflow 작성
- pushlish (w. `@Changesets` )

[https://github.com/homiekim/demo-package](https://github.com/homiekim/demo-package)

[https://www.npmjs.com/package/@siper/demo-package](https://www.npmjs.com/package/@siper/demo-package)

가이드가 굉장히 친절하고 쉽게 되어있지만 처음 들어보거나 얕게 알고 있었던 부분이 많았던 것 같음

오히려 기본적인 package.json 설정이나 tsconfig같은걸 얕게 알고 있었던 부분이 많았음

반성하고 기본적인 걸 복습 할 수 있는 기회가 된 것 같다

https://poiemaweb.com/nodejs-npm

### 처음 들어보거나 배운 것들

- package.json 설정 필드 값들 중 제대로 모르고 있었던 것들..
- tsconfig 이해
- 첨들어본 라이브러리들
    - `@arethetypesworng` , `@tsup` , `@Changesets`
- Dual Package Hazard ⇒ 듀얼 패키지 지원이 무조건 좋은 건 줄 알았음https://github.com/GeoffreyBooth/dual-package-hazard
- 시맨틱 버전 정확히 알고 넘어가쟈~  https://semver.org/
    
    (learna는 모노레포 관리를 위한 것)
    

### 조금 더 알아보자

- package.json 설정들
    - package.json
        
        ```json
        {
          "name": "@siper/demo-package",
          "version": "1.0.1",
          "description": "package publish test",
          "main": "dist/index.js",
          "scripts": {
            "build": "tsup",
            "ci": "npm run build && npm run check-format && npm run check-exports && npm run lint && npm run test",
            "format": "prettier --write .",
            "check-format": "prettier --check .",
            "check-exports": "attw --pack . --ignore-rules=cjs-resolves-to-esm",
            "lint": "tsc",
            "test": "vitest run",
            "local-release": "changeset version &&changeset publish",
            "prepublishOnly": "npm run ci"
          },
          "exports": {
            "./package.json": "./package.json",
            ".": {
              "import": "./dist/index.js",
              "default": "./dist/index.cjs"
            }
          },
          "keywords": [],
          "author": "homie",
          "license": "MIT",
          "files": [
            "dist"
          ],
          "type": "module",
          "devDependencies": {
            "@arethetypeswrong/cli": "^0.16.4",
            "@changesets/cli": "^2.27.9",
            "prettier": "^3.3.3",
            "tsup": "^8.3.5",
            "typescript": "^5.6.3",
            "vitest": "^2.1.4"
          }
        }
        
        ```
        
    - `main` : 패키지의 진입점(entry point), CommonJS 형식으로 불러올 때의 진입점 파일. `require`를 통해 이 파일을 불러올 수 있음.
    - `export`  : (npm 최신버전에서 동작하는듯?) main 대신에 여러 진입점을 제공할 수 있는 기능, exports 이외의 다른 진입점을 방지하는 기능
    
    [https://nodejs.org/api/packages.html#package-entry-points](https://nodejs.org/api/packages.html#package-entry-points)
    이거보면 좋음
    
    - gpt 형 도와줘..
        - **다양한 진입점 정의**:
            - `exports` 필드는 패키지에 대해 여러 개의 진입점을 정의할 수 있습니다. 예를 들어, 모듈이 다양한 환경에서 다르게 작동해야 할 경우, 각 환경에 맞는 진입점을 설정할 수 있습니다. 이는 동일한 패키지가 ES 모듈 방식으로 불러올 때와 CommonJS 방식으로 불러올 때 각각 다른 파일을 참조하도록 설정할 수 있게 해줍니다.
        - **조건부 진입점 해상도**:
            - `exports`는 환경에 따라 진입점을 조건부로 정의할 수 있는 기능을 제공합니다. 예를 들어, `require`를 통해 불러올 때와 `import`를 사용할 때 각각 다른 파일로 연결될 수 있도록 할 수 있습니다. 이를 통해 특정 환경에서만 필요한 코드를 포함하거나 제외할 수 있습니다.
        - **공식 인터페이스 정의**:
            - `exports`를 사용하면 모듈 작성자가 패키지의 공개 인터페이스를 명확하게 정의할 수 있습니다. 이를 통해 사용자들이 어떤 API가 공개되어 있는지를 분명하게 알 수 있으며, 패키지의 안정성을 높이는 데 기여합니다.
        - **진입점 제한**:
            - `exports` 필드에 정의되지 않은 진입점은 사용할 수 없게 되므로, 사용자가 정의된 공개 API만 사용할 수 있습니다. 예를 들어, 사용자가 `require('your-package/package.json')`과 같이 접근하는 것을 차단할 수 있습니다. 이는 모듈의 내부 구조가 노출되는 것을 방지합니다.
        - **기존 패키지의 변화**:
            - 기존 패키지에서 `exports` 필드를 도입할 경우, 사용자가 이전에 사용했던 모든 진입점이 정의되어 있어야 하며, 그렇지 않을 경우 호환성 문제가 발생할 수 있습니다. 따라서, 모든 이전에 지원되던 진입점을 `exports`에 포함시키는 것이 좋습니다.
        - **추천하는 사용**:
            - 새로운 패키지를 만들 때는 현재 지원되는 Node.js 버전을 대상으로 할 경우, `exports` 필드를 사용하는 것이 권장됩니다. 반면에 Node.js 10 이하 버전을 지원해야 할 경우에는 `main` 필드가 필요합니다. 만약 `exports`와 `main` 둘 다 정의되어 있다면, 지원되는 Node.js 버전에서는 `exports`가 우선 적용됩니다.
    - `license` : 패키지 사용자들이 당신이 만든 패키지를 사용하기 위해 어떻게 권한을 얻었는지 또 어떤 금기 사항이 있는지 알게 하기 위해 라이센스를 사용 
    https://choosealicense.com/licenses/
    - `files` : 패키지를 설치할 때 포함할 파일 목록을 지정합니다. 이 필드를 사용하면 특정 파일만 포함하거나 제외할 수 있습니다. ⇒ 불필요한 파일은 제외
- tsconfig
- Semver
    - [https://semver.org/](https://semver.org/)
    
    ![image.png](node%20hero%201week%20note%201331cb32c82480618de4d6abf4160081/image.png)
    
    - 기존 버전과 호환되지 않게 API가 바뀌면 Major Version 을 올리고,
    - 기존 버전과 호환되면서 새로운 기능을 추가할 때는 Minor Version 을 올리고,
    - 기존 버전과 호환되면서 버그를 수정한 것이라면 Patch Version 을 올린다.
- `@aretheTypesworng`
    - 패키지 내의 정적 코드 분석 도구인듯? 타입 검사나 module resolution issue를 잡아주는 도구
- `@tsup`
    - webpack, rollup 같은 번들러인듯? 가이드에서  dual package support를 하게 해줌
    `This is a tool built on top of **esbuild** that compiles your TypeScript code into both formats`
    - rollup 보다 뭐가 더 좋은지 모르겠음? 조금더 알아 봐야 할 듯?
- `@changeset`

### ToBe ??

- 모노레포 구성 에서 패키지 배포 (pnpm, rollup, learna)
- 가이드보다 조금도 구체화된 모노레포 아키텍처를 구성해 보고싶음
- 그래서 어떤 라이브러리를 만들고 싶은가,,? (굉장히 러프한 아이디어)
    - 리액트 컴포넌트
        - ui를 위한 캘린더, datepicker이런거 만들면 진짜 유용할 것 같은데 리소스가 많이 들것 같음
        - 애초에 내가만든 컴포넌트나 훅이 리액트에서 동작하게 하는 것이 1차 목표
        - 리액트 버전이나 디펜던시 충돌 같은 문제가 없게 하려면 ??
        - 그러면 간단한 상태관리 라이브러리를 만들어보고싶음
        
         
        
- 테스트코드도 실무에서 작성경험이 거의 없는데 이번기회에 꼼꼼하게 작성해보면 좋을 듯!