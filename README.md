# 📊 kyeol-saleor-dashboard

> **KYEOL Saleor Dashboard - React 기반 관리자 대시보드**

---

## 📌 이 레포는 무엇을 하는가

Saleor GraphQL API를 사용하는 **관리자용 대시보드**입니다.

**주요 기능**:
- 상품/주문/고객 관리
- 재고 관리
- 마케팅/할인 설정
- 사용자 권한 관리

**기술 스택**:
- React 18+
- TypeScript
- Apollo Client (GraphQL)
- Material-UI

---

## 👤 언제 / 누가 / 왜 사용하는가

| 상황 | 사용 여부 |
|------|:--------:|
| 대시보드 UI 개발 | ✅ 사용 |
| 새 기능 추가 | ✅ 사용 |
| Kubernetes 배포 | ❌ 미사용 (kyeol-app-gitops 사용) |

---

## 🏛️ 전체 아키텍처에서의 위치

```
[이 레포] kyeol-saleor-dashboard
    ↓ (GitHub Actions: Docker Build & Push)
[ECR] min-kyeol-*-dashboard:*-latest
    ↓ (이미지 참조)
[kyeol-app-gitops] Deployment 배포
    ↓
[EKS] Pod 실행
    ↓
[인터넷] *-dashboard-kyeol.msp-g1.click
```

---

## 📁 주요 디렉터리 설명

```
kyeol-saleor-dashboard/
├── src/                   # 소스 코드
│   ├── components/       # React 컴포넌트
│   ├── pages/            # 페이지 컴포넌트
│   └── graphql/          # GraphQL 스키마/쿼리
├── .github/
│   └── workflows/
│       └── build-push-dashboard-ecr.yml  # ECR 빌드/푸시
├── Dockerfile             # 컨테이너 이미지 정의
└── vite.config.js         # Vite 설정
```

---

## ⚠️ 주의사항

### 🔧 로컬 개발

```powershell
npm install
npm run dev  # localhost:9000
```

### 🔧 빌드 시 API_URL 필요

Dashboard는 빌드 시점에 API URL이 필요합니다:
```powershell
API_URL=https://your-saleor-api.com/graphql/ npm run build
```

---

## 🔗 다른 레포와의 관계

| 레포지토리 | 관계 |
|-----------|------|
| kyeol-app-gitops | 이 레포의 이미지를 배포 |
| kyeol-infra-terraform | ECR 레포지토리 생성 |

---

## 🚀 CI/CD (GitHub Actions)

`main` 브랜치 push 시 자동 실행:
- DEV, STAGE, PROD 환경별 빌드 (환경별 API_URL 적용)
- 환경별 ECR 레포지토리에 push

**태그 규칙**: `{env}-latest`, `{env}-{commit-sha}`

---

> **마지막 업데이트**: 2026-01-03
