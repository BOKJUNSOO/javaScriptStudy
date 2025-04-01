## React

### 개발환경
`vs code` + `nodejs(npm)` 의 조합으로 환경을 구성한다

### 프로젝트 생성
`create-react-app` - cra

과거에는 `npm` 을 통해서 설치했는데, 현재 `npx` 사용을 권장한다.

1. `nodejs 설치` (`npm, npx 같이 설치`)

2. 프로젝트 생성
    - `npx create-react-app [프로젝트이름]` (`node_modules`) 대략 200메가 이상

3. 프로젝트 실행
    - `nodejs`

4. 프로젝트 완료후 `deploy`
   (용량이 줄어듦)

```bash
npx create-react-app react-app
```

### 프로젝트 디렉토리

- `node_modules`: 라이브러리 폴더
- `public` : 이미지 파일과 같은 `static` 파일 보관함, 빌드 시에 압축되지 않음
- `src` : 소스코드 보관함
- `App.js` : 메인페이지에 들어갈 `HTML`을 작성하는 곳

### 리액트 어플리케이션의 흐름
- `npm start run` 을 통해 어플리 케이션에 진입한다.
- `index.js`가 먼저 실행이 된다.
- 이후 `App.js` 에 작성된 `HTML`이 랜더링 되어
- 해당 내용이 `index.html`에 할당된다