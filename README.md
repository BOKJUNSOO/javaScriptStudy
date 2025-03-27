# javaScriptStudy
`June Soo's JavaScript + git convetion Study Repo😋`

## Repo 구성
- git convention 지키면서 push 하기

- 디렉터리 정리
    - `PDF` 하나당 폴더 하나씩 사용
    - `PDF` 하나당 `.md` 는 카테코리별 분류
    - `javascript` 소스코드는 `src` 로 따로 관리

## git convention

- 기본적인 `commit Message Structure` 은 다음과 같다.
```markdown
`제목(Type: Subject)`
(한줄 띄어 분리)
본문 (Body)
(한줄 띄어 분리)
꼬리말 (Footer)
```

1. `Commit Type`
```markdown
태그: 제목
`:` 뒤에만 스페이스를 둔다
```

|태그 종류| 태그설명|
|--|--|
|Feat|새로운 기능을 추가|
|Fix|버그 수정|
|Design|CSS 등 사용자 UI 디자인 변경|
|!BREAKING CHANGE|커다란 API 변경의 경우
|!HOTFIX|급하게 치명적인 버그를 고쳐야 하는 경우|
|Style|코드 포맷 변경, 세미 콜론 누락, 코드 수정이 없는 경우|
|Refactor|프로덕션 코드 리팩토링|
|Comment| 필요한 주석 추가 및 변경|
|Docs|문서 수정|
|Test|테스트 코드, 리팩토링 테스트 코드 추가, Production Code 변경 없음|
|Chore| 빌드 업무 수정, 패키지 매니저 수정, 패키지 관리자 구성 등 업데이터, Production Code 변경 없음|
|Rename| 파일 혹은 폴더명을 수정하거나 옮기는 작업만인 경우|
|Remove| 파일을 삭제하는 작업만 수행한 경우

2. `Subject`

- 제목은 50글자 이내로 작성한다
- 개조식 구문으로 작성한다
- 마침표 및 특수기호는 사용하지 않는다.

- 영문으로 작성하는 경우
  - 동사 원형을 가장 앞에 명령어로 작성한다.
  - 첫글자는 대문자로 작성한다

<dr>

3. `Body`

- 72이내로 작성한다
- 최대한 상세히 작성한다 (코드 변경의 이유를 명확히 작성한다.)
- 어떻게 변경했는지 보다는 "무엇을, 왜" 변경했는지 작성한다.

<dr>

4. `Footer`

- 선택사항
