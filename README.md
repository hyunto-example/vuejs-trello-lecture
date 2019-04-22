# 트렐로 개발을 통한 Vuejs, Vuex, Vue-Router 프론트엔드 실전 기술

[인프런 - 트렐로 개발을 통한 Vuejs, Vuex, Vue-Router 프론트엔드 실전 기술 (김정환 강사)](https://www.inflearn.com/course/vuejs/)

## 사용 기술

- Vue.js
- Vuex
- Vue-Router
- Axios
- Dragular

## 분석

### 요구사항 분석

- 인증
  - 로그인
    - 실패시 에러 메세지 출력
  - 로그아웃
- 메인 페이지
  - 보드 목록
  - 보드 생성
    - 보드 입력 폼 - 보드 색상 선택
- 보드
  - 리스트
    - 리스트 출력
    - 리스트 내에 카드 출력
    - 리스트 추가
    - 리스트 제거
    - 리스트 이름 수정
    - 리스트 순서 변경
  - 카드
    - 카드 생성
    - 카드 내용 출력 - 모달
    - 카드 내용 수정
    - 카드 삭제
    - 리스트 내에서 카드 순서 변경
    - 각 리스트 간 카드 이동
  - 사이드바
    - 사이드바 보이기 / 안보이기
    - 보드 배경 변경
    - 보드 삭제

### 기본 플로우

1. 홈페이지 접속
2. 로그인 페이지
3. 홈페이지 리다이렉트
4. 보드 목록 조회
5. 보드 생성
6. 보드 조회 : Todo, Doing, Done 리스트 생성
7. 카드 생성
8. 카드 상세 조회 (모달)
9. 카드 수정 (모달)
10. 카드 이동
11. 카드 삭제
12. 보드 설정 : 배경
13. 보드 삭제 후 홈페이지 이동

### 추가 기능

- 보드 수정 : 색상 변경
- 보드 수정 : 타이틀 변경
- 리스트 생성
- 리스트 수정 : 타이틀 변경
- 리스트 이동
- 리스트 삭제

## 코드 스캐폴딩

### 프로젝트 생성

```bash
$ npm install -g @vue/cli
$ vue create vuejs-trello-lecture
	Vue CLI v3.6.3
	? Please pick a preset: default (babel, eslint)
	...생략...
 
$ npm run serve
```

### 프로젝트 사용법

To customize configuration, See [Configuration Reference](https://cli.vuejs.org/config/).

```bash
## Project setup
npm install

### Compiles and hot-reloads for development
npm run serve

### Compiles and minifies for production
npm run build

### Run your tests
npm run test

### Lints and fixes files
npm run lint
```

