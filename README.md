# cxr542-launcher

팀장용 **Workspace 랜딩** — [교육팀 TMS](https://github.com/cxr542/edu-team-tms) · [cxr542-portal](https://github.com/cxr542/cxr542-portal) 두 앱으로만 연결합니다.

| 환경 | URL |
|------|-----|
| 운영 | https://cxr542-launcher.vercel.app |
| 로컬 | http://localhost:4321 |

## 개발

```bash
npm run dev
```

TMS·Portal에서 `← Workspace` 링크는 운영 시 위 URL을 사용합니다.  
로컬 개발 시 각 앱에 `VITE_LAUNCHER_ORIGIN=http://localhost:4321` (선택).

## 배포

- **Vercel** 프로젝트 `cxr542-launcher` (정적 `index.html`)
- GitHub Actions: `.github/workflows/deploy-production.yml`
- Secrets: `VERCEL_TOKEN`, `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`

수동 배포:

```bash
npx vercel deploy --prod
```

## 관련 repo

| Repo | 역할 |
|------|------|
| `edu-team-tms` | 교육팀 업무 |
| `cxr542-portal` | 개인 포털 |
| `cxr542-launcher` | 이 랜딩 (허브) |

TMS에 있던 목업 HTML은 이 repo로 이전되었습니다. TMS `public/preview/` 는 개발 fallback용으로만 유지할 수 있습니다.
