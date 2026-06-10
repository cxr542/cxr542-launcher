# cxr542-launcher

팀장용 **Workspace 랜딩** — [교육팀 TMS](https://github.com/cxr542/edu-team-tms) · [cxr542-portal](https://github.com/cxr542/cxr542-portal) 두 앱으로 빠르게 진입하기 위한 운영 런처입니다.

| 환경 | URL |
|------|-----|
| 운영 | https://cxr542-launcher.vercel.app |
| 로컬 | http://localhost:4321 |

## 목적

`cxr542-launcher`는 교육팀 업무 화면과 개인 개발 포털을 한 곳에서 여는 개인/팀장용 허브입니다.  
브라우저 북마크나 iPhone 홈 화면에 추가해두고, 매번 TMS와 Portal 주소를 따로 찾지 않도록 하는 것이 목적입니다.

## 연결 서비스

| 서비스 | URL | 역할 |
|------|-----|------|
| 교육팀 TMS | https://okestro-edu-team-tms.vercel.app/ | 장부, 일일 업무일지, KPI, 점심, Academizer, 참고문서 등 교육팀 운영 업무 |
| cxr542-portal | https://cxr542-portal.vercel.app/ | 아이디어뱅크, vision-font, today-shoes, 마라톤 등 개인 모듈과 개발 포털 |

## iPhone 홈 화면 추가

1. iPhone에서 Safari로 https://cxr542-launcher.vercel.app 접속
2. 하단 공유 버튼 선택
3. **홈 화면에 추가** 선택
4. 이름을 `AI학습허브` 또는 `cxr542 런처`로 저장

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
