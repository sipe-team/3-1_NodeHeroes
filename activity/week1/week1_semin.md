# 1주차 활동 정리

'NODE HEROES'의 앞으로의 활동을 미리 경험해보기 위해, 이번 주에는 간단한 npm 패키지 데모 버전을 제작 및 배포해보는 활동을 진행했습니다.
학습 자료는 은비님께서 추천해 주신 [How To Create An NPM Package](https://www.totaltypescript.com/how-to-create-an-npm-package) 가이드를 참고했습니다.

- **Repository**: [npm-package-demo](https://github.com/SEMIN-97/npm-package-demo)
- **Demo Package**: [npm-package-demo-semin](https://www.npmjs.com/package/npm-package-demo-semin)

아래는 가이드를 바탕으로 추가로 공부한 내용을 정리한 것입니다.

---

## @arethetypeswrong/cli
`@arethetypeswrong/cli`는 타입스크립트 타입 정의가 올바르게 작동하는지 검사하는 도구입니다. CommonJS(CJS)와 ESModule(ESM) 간의 호환성 문제를 파악할 수 있게 도와줍니다.

```
attw --pack . --ignore-rules=cjs-resolves-to-esm
```
- **`--pack`**: 현재 디렉토리를 패키지로서 검사합니다.
- **`.`**: 현재 디렉토리에서 attw 명령이 동작하게 지정합니다.
- **`--ignore-rules=cjs-resolves-to-esm`**: CJS가 ESM으로 해결된다는 규칙을 무시하여, 패키지를 ES 모듈 전용으로 설정하고 CJS 관련 오류를 방지합니다.

### CJS 지원을 하지 않는 이유
- **단순화**: ES 모듈을 사용하면 모듈 로딩이 더 간단하고 최신 JavaScript 기능을 지원합니다.
- **호환성 문제 감소**: CJS와 ESM 혼용 시 발생할 수 있는 호환성 문제를 줄여줍니다.
- **최신 표준 사용**: ES 모듈은 JavaScript의 최신 표준으로, 성능 및 효율성 측면에서도 장점을 가지고 있습니다.
 
## Changesets
Changesets은 패키지 변경 사항 추적과 배포 준비에 필요한 도구입니다. 버전 관리, 변경 로그 작성, 배포 자동화 등을 돕습니다.

### 주요 개념 및 사용 방법

1. **Changeset 생성** (`npx changeset`):
    - 이 명령어를 실행하면 **변경 사항에 대한 설명을 기록**할 수 있습니다.
    - `patch`, `minor`, `major` 중 하나의 버전 유형을 선택하고 변경 사항 설명을 작성합니다.
    - 완료 시 `.changeset` 폴더에 고유한 이름의 Markdown 파일이 생성되며, 이 파일이 변경 로그의 기초가 됩니다.
    - changeset 파일은 `empty-lizards-give.md` 같은 랜덤한 단어 조합으로 이름이 생성됩니다. 이는 변경 사항을 유니크하게 구분하기 위한 장치입니다.
2. **변경 사항 누적 및 버전 올리기** (`changeset version`):
    - 여러 changeset 파일을 기반으로 프로젝트의 패키지 버전을 자동으로 업데이트합니다.
     - 이 과정에서 `package.json`과 `CHANGELOG.md`가 업데이트됩니다.
3. **배포 및 릴리스 노트 생성** (`changeset publish`):
    - 배포 명령어로 changeset 파일의 내용을 npm에 배포합니다.
    - GitHub Actions 같은 CI/CD와 연동하면, 변경 사항이 자동으로 릴리스 노트에 반영됩니다.

### 최종 변경 로그와 릴리스 노트
- 각 changeset 파일에 적힌 내용은 최종 릴리스 시 **CHANGELOG.md**에 반영되고, GitHub 릴리스 노트에도 포함됩니다. 추가 설명을 작성하여 사용자에게 유용한 정보를 충분히 제공할 수 있습니다.

---

## 후기 🏃
추천받은 가이드가 A-Z까지 적혀있어 어렵지 않게 잘 따라간 것 같습니다. 이번에 한 사이클을 경험해 본 덕분에 실제 패키지를 제작할 때도 크게 헤매지 않고 만들 수 있을 것 같아요👍

물론, 가이드가 응축되어 있는 만큼 세세한 건 실제로 부딪히며 공부해 보겠습니다!

모두 화이팅🔥
