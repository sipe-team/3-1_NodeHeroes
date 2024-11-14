# 🐸 Npm 패키지 개발 일지

### 시작하며

이전에 선정한 주제가 도움은 될 것 같으나, 자꾸만 회사에서 쓸만한걸 만드려고 하니 지루해졌다...! 그래서 좀 더 재미있는 걸 개발하고 싶어서 구글링하며 좀 . 더재밌는 패키지들이 있나 살펴보았다. 월말에는 아마 거의 풀야근 일정이 잡혀있어서, 최대한 단순하면서도 재미있어보이는걸 하려고 했다.

---

### 후보로 발견한 Npm 패키지들

구글링 중에 발견한 재미있는 Npm 패키지들 몇 가지를 정리해 보았다:

- [colors.js](https://www.npmjs.com/package/colors): 콘솔 텍스트에 다양한 색을 추가할 수 있는 라이브러리.
- [faker.js](https://www.npmjs.com/package/faker): 무작위로 데이터를 생성해주는 라이브러리.
- [chalk](https://www.npmjs.com/package/chalk): 터미널에서 문자열 스타일링을 간편하게 할 수 있는 패키지.
- [cowsay](https://www.npmjs.com/package/cowsay): ASCII 아트로 소가 말을 하는 재미있는 패키지.
- [figlet](https://www.npmjs.com/package/figlet): 텍스트를 멋진 ASCII 아트로 변환하는 패키지.

---

### 최종 선택: cowsay 🐄

고민 끝에 **cowsay**라는 패키지를 선택했다.
이미 catsay, dogsay 같이 비슷한 기능을 하는 패키지들이 다른 버전(?)으로 여럿 나온 것을 보기도 했고, 그냥 눈이 갔다.
ASCII 아트로 소가 말을 하는 기능은 단순하지만 매력적이고, 뭔가 더 귀엽고 창의적인 걸 추가할 아이디어도 떠올릴 수 있을 것 같았다!

#### cowsay란?

cowsay는 명령어로 입력한 텍스트를 귀여운 소 ASCII 아트와 함께 출력해주는 패키지다. 기본적으로 아래와 같은 형태로 동작한다:

```bash
npx cowsay "Hello, World!"
```

출력은 아래와 같이 된다.

```
 _________
< Hello, World! >
 ---------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

```

귀엽다! 다른 버전으로 만들어보자.
