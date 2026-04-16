<div align="center">

# 같이가자 (Gachi-Gaja)

<p>
  <img src="https://img.shields.io/badge/Stack-React%20%7C%20Vite%20%7C%20TailwindCSS-3B82F6?style=for-the-badge" alt="Stack Badge" />
  <img src="https://img.shields.io/badge/UI-Radix%20UI%20%7C%20shadcn%2Fui-6366F1?style=for-the-badge" alt="UI Badge" />
  <img src="https://img.shields.io/badge/Deploy-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Deploy Badge" />
</p>

<p>
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1e3a8a,50:3b82f6,100:93c5fd&height=220&section=header&text=Gachi%20Gaja&fontSize=44&fontColor=ffffff&animation=fadeIn&fontAlignY=35" width="100%" alt="banner" />
</p>

<p>
  <strong>단체 여행 계획 서비스 — 같이가자</strong><br/>
  <sub>의견 수집부터 AI 일정 생성, 투표, 확정까지 한 번에</sub>
</p>

</div>

## 프로젝트 한 줄 소개

여행 그룹을 만들고, 구성원의 요구사항을 수집한 뒤 AI가 후보 일정을 생성하면 투표로 확정하는 단체 여행 계획 AI 서비스입니다.

## 하이라이트

- `그룹 생성 & 초대 링크` 기반 멤버 참여 구조
- `요구사항 수집` → `AI 후보 일정 자동 생성` → `투표 확정` 플로우
- `React + Vite` SPA 기반 빠른 개발 환경
- `Radix UI / shadcn/ui` 컴포넌트 시스템

## 핵심 기능

### 1. 회원가입 / 로그인
- 이메일 + 비밀번호 기반 인증
- 로그인 후 `userId`를 localStorage에 저장하여 이후 API 요청에 활용

### 2. 여행 그룹 관리
- 그룹 생성, 수정, 삭제
- 초대 링크로 멤버 참여
- 내 그룹 목록 조회 (호스트/멤버 역할 구분)

### 3. 요구사항 수집
- 그룹 내 각 멤버가 여행 요구사항(텍스트) 등록, 수정, 삭제
- 수집된 요구사항을 바탕으로 AI 후보 일정 생성 요청

### 4. AI 후보 일정 생성 & 투표
- 백엔드 AI가 요구사항을 분석해 복수의 후보 일정을 자동 생성
- 구성원이 선호 일정에 투표 → 투표 요약 조회

### 5. 확정 일정 관리
- 투표로 결정된 일정 확정
- 확정 이후에도 수정 가능

## 아키텍처

```text
사용자 브라우저
   ↓
React SPA (Vite)
   ↓
Axios API Client (/api 프록시)
   ├── /users, /login, /logout
   ├── /groups, /groups/:id
   ├── /groups/:id/requirements
   ├── /groups/:id/candidates
   └── /groups/:id/candidates/votes
```

## 기술 스택

<p>
  <img src="https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=white" alt="React" />
  <img src="https://img.shields.io/badge/Vite-6-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/TailwindCSS-4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="TailwindCSS" />
  <img src="https://img.shields.io/badge/Radix_UI-shadcn-000000?style=for-the-badge" alt="Radix UI" />
  <img src="https://img.shields.io/badge/React_Router-7-CA4245?style=for-the-badge&logo=reactrouter&logoColor=white" alt="React Router" />
  <img src="https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white" alt="Axios" />
  <img src="https://img.shields.io/badge/React_Hook_Form-EC5990?style=for-the-badge" alt="React Hook Form" />
  <img src="https://img.shields.io/badge/Zod-3E67B1?style=for-the-badge" alt="Zod" />
  <img src="https://img.shields.io/badge/MSW-FF6A33?style=for-the-badge" alt="MSW" />
  <img src="https://img.shields.io/badge/Vercel_Analytics-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Vercel Analytics" />
</p>

## 저장소 구성

```text
.
├── src/
│   ├── api/                 # Axios API 클라이언트 및 도메인별 API 함수
│   │   ├── client.js        # Axios 인스턴스 (인터셉터 포함)
│   │   ├── auth.js          # 회원가입 / 로그인 / 로그아웃
│   │   ├── group.js         # 그룹 CRUD, 멤버 관리
│   │   ├── requirements.js  # 요구사항 CRUD
│   │   └── candidates.js    # AI 후보 생성 및 투표
│   ├── components/
│   │   ├── ui/              # shadcn/ui 기반 공통 컴포넌트
│   │   └── header.jsx       # 공통 헤더
│   ├── pages/
│   │   ├── LandingPage.jsx            # 로그인 / 회원가입
│   │   └── rooms/
│   │       ├── page.jsx               # 내 그룹 목록
│   │       ├── create/page.jsx        # 그룹 생성
│   │       └── [id]/
│   │           ├── page.jsx           # 그룹 상세
│   │           ├── edit/page.jsx      # 그룹 수정
│   │           ├── confirmed/page.jsx # 확정 일정
│   │           ├── confirmed/edit/    # 확정 일정 수정
│   │           └── plans/page.jsx     # 일정(플랜)
│   ├── router/router.jsx    # React Router 라우팅 설정
│   ├── mocks/               # MSW 목 핸들러
│   ├── lib/                 # 유틸리티 함수
│   └── main.jsx             # 앱 진입점
├── public/                  # 정적 파일
├── vite.config.js
└── package.json
```

## 실행 방법

### 1. 의존성 설치

```bash
npm install
```

### 2. 개발 서버 실행

```bash
npm run dev
```

기본 포트: `http://localhost:5173`

### 3. 프로덕션 빌드

```bash
npm run build
```

## 환경 변수 예시

```bash
# 백엔드 API 서버 주소 (vite.config.js에서 /api 프록시로 연결)
VITE_API_BASE_URL=http://localhost:8080
```

## 주요 API

- `POST /users` — 회원가입
- `POST /login` — 로그인
- `POST /logout` — 로그아웃
- `GET /groups` — 내 그룹 목록 조회
- `POST /groups` — 그룹 생성
- `GET /groups/:id` — 그룹 상세 조회
- `PUT /groups/:id` — 그룹 수정
- `DELETE /groups/:id` — 그룹 삭제
- `GET /groups/:id/members` — 멤버 목록 조회
- `POST /groups/:id/members` — 멤버 추가
- `GET /groups/:id/requirements` — 요구사항 목록
- `POST /groups/:id/requirements` — 요구사항 등록
- `PUT /groups/:id/requirements/:reqId` — 요구사항 수정
- `DELETE /groups/:id/requirements/:reqId` — 요구사항 삭제
- `POST /groups/:id/candidates` — AI 후보 일정 생성
- `GET /groups/:id/candidates/votes` — 투표 요약 조회
- `POST /groups/:id/candidates/votes` — 투표

## GitHub

- Repository: https://github.com/blackwellSW/Gachi-Gaja-FE

## 라이선스

MIT License
