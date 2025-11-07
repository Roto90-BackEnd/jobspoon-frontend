# 🥄 Jobspoon - Frontend (MFE Monorepo)

[![React](https://img.shields.io/badge/React-18.x-blue)](https://reactjs.org/)
[![Vue.js](https://img.shields.io/badge/Vue.js-3.x-brightgreen)](https://vuejs.org/)
[![Svelte](https://img.shields.io/badge/Svelte-4.x-orange)](https://svelte.dev/)
[![Lerna](https://img.shields.io/badge/managed%20by-Lerna-blueviolet)](https://lerna.js.org/)
[![Docker](https://img.shields.io/badge/Docker-ready-blue)](./Dockerfile)
[![Project Period](https://img.shields.io/badge/Project%20Period-2025.07%20~%202025.10-informational)](...)

Jobspoon은 IT 취업 준비생을 위한 **AI 면접 솔루션 및 스터디 플랫폼**입니다.
본 레포지토리는 Jobspoon 서비스의 **프론트엔드**입니다.

## 🏛️ 아키텍처: "Polyglot" Micro-Frontends (MFE)

본 프로젝트는 **Lerna**를 사용하여 여러 개의 독립적인 프론트엔드 패키지를 관리하는 **모노레포(Monorepo)** 구조를 따릅니다.

특히, 각 핵심 기능(스터디, 면접 등)은 **React, Vue, Svelte** 등 각 도메인에 가장 적합한 프레임워크를 사용하여 별도의 마이크로-프론트엔드(MFE) 패키지로 분리되어 있습니다.

## 📦 패키지 구조 (Lerna)

모든 MFE 앱과 라이브러리는 **"플랫(Flat)" 구조**로 루트 디렉토리에서 관리됩니다.

```bash
jobspoon-frontend/
├── 📁 docker/               # (Docker-compose, Nginx configs, etc.)
├── 📁 main-container/       # (메인 셸(Shell) App)
├── 📁 mypage-app/           # (마이페이지 Micro-App)
├── 📁 navigation-bar-app/   # (공통 네비게이션 Micro-App)
├── 📁 packages/             # (Lerna package for common/shared code)
├── 📁 spoon-word-app/       # (스푼워드 Micro-App)
├── 📁 studyroom-app/        # (스터디룸 Micro-App - React)
├── 📁 svelte-review-app/    # (Svelte PoC)
├── 📁 sveltekit-review-app/ # (SvelteKit PoC)
├── 📁 vue-account-app/      # (계정/인증 Micro-App - Vue)
├── 📁 vue-ai-interview-app/ # (AI 모의면접 Micro-App - Vue)
├── 📄 Dockerfile           # (Root Dockerfile for container)
├── 📄 lerna.json           # (Lerna 모노레포 configuration)
└── 📄 package.json          # (Root package.json & scripts)

## 🛠️ 기술 스택 (Tech Stack)

| Category | Stack | Description |
| :--- | :--- | :--- |
| **Language** | TypeScript (v5.9.2) | |
| **Framework** | React (v18.3.1), Vue.js, Svelte | "Polyglot" - MFE별 최적의 프레임워크 사용 |
| **Architecture** | Micro-Frontends (MFE) | 기능별 독립적인 프론트엔드 패키지 구성 |
| **Monorepo** | Lerna | 다중 패키지 빌드 및 종속성 관리 |
| **Styling** | Styled-Components | 컴포넌트 기반 CSS-in-JS |
| **API Client** | Axios | 백엔드 API 통신 (with Interceptors) |
| **Container** | Docker | `Dockerfile`을 통한 프론트엔드 서버 컨테이너화 |
| **Build** | [Vite / Webpack] | [사용한 번들러/빌드 도구] |


## 🚀 로컬 실행 방법 (Getting Started)

### 1. 전제 조건 (Prerequisites)

* [Node.js](https://nodejs.org/ko) (v18.x 이상)
* [NPM](https://www.npmjs.com/)
* (필수) **백엔드 서버**가 로컬(`http://localhost:8080`)에서 실행 중이어야 함

### 2. 실행 가이드 (Running Locally)

1.  **레포지토리 클론**
    ```bash
    git clone [[https://github.com/Your-Frontend-Repo-URL](https://github.com/Your-Frontend-Repo-URL)]
    cd [frontend-repo-name]
    ```

2.  **의존성 설치 (Lerna Bootstrap)**

    Lerna 모노레포의 모든 패키지 의존성을 한 번에 설치합니다.
    ```bash
    npm install
    ```
    *(NPM이 `lerna bootstrap`을 자동으로 실행합니다.)*

3.  **환경변수 파일 생성 (`.env`)**

    > 💡 .env 파일 관리
    > MFE 구조의 각 패키지(main-container, studyroom-app 등)는 자신만의 .env 파일이 필요합니다.
    > 각 패키지 폴더 내부의 .env.example 파일을 .env로 복사하고, 필요한 API 주소(e.g., VITE_API_URL=http://localhost:8080)를 설정해야 합니다.
    > 각 패키지(e.g., `packages/study`)를 개별 실행해야 할 경우, 해당 패키지 내부의 `.env.example`과 `README.md`를 참고하세요.

4.  **로컬 서버 실행**

    프로젝트 루트에서 `start` 스크립트를 실행합니다. (Lerna가 모든 패키지를 동시에 실행합니다.)
    ```bash
    npm run start
    ```

5.  **확인**
    * 브라우저에서 `http://localhost:3000` (컨테이너 App)으로 접속합니다.

## 🔗 백엔드 API
본 프론트엔드 프로젝트는 Jobspoon-Spring-Backend 레포지토리에 정의된 API를 사용합니다.

백엔드 레포지토리: https://github.com/Roto90-BackEnd/jobspoon-spring-backend

API 명세서 (Swagger): http://localhost:8080/swagger-ui.html

⚠️ Known Issue

현재 백엔드 Spring Boot 3.5.3 버전과 springdoc:2.5.0 라이브러리 간의 호환성 이슈로 인해, /swagger-ui.html 엔드포인트가 500 Internal Server Error를 반환하고 있습니다.

[임시 조치]

API 테스트가 필요한 경우, Postman이나 HTTPie 같은 별도의 API 클라이언트를 사용해 주시기 바랍니다.

(또는, 백엔드 레포지토리의 README를 참고하여 호환성 문제 해결이 필요합니다.)
