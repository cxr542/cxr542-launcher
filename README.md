# cxr542-ai-workspace

`cxr542-launcher`는 **cxr542-ai-workspace** 허브를 여는 런처입니다.
교육팀 운영, 개인/팀 AI 포털, 실험/아이디어, 운영 신호를 한 곳에서 관리하는 진입점으로 사용합니다.

| 환경 | URL |
|------|-----|
| 운영 | https://cxr542-launcher.vercel.app |
| 로컬 | http://localhost:4321 |

## Purpose

이 저장소는 개인/팀 AI 작업 허브의 런처입니다.
브라우저 북마크나 iPhone 홈 화면에 추가해두고, EDU-TMS와 AI 포털/아이디어 허브를 빠르게 여는 것이 목적입니다.

## Current Status

- `cxr542-launcher`는 실제 배포 리포지토리 이름입니다.
- 런처 화면은 `cxr542-ai-workspace` 허브로 안내합니다.
- 현재 live 하위 앱으로는 `cxr542-portal`이 유지됩니다.
- 일부 하위 앱은 준비 중일 수 있으므로 README에서 상태를 함께 관리합니다.

## Apps

### okestro-edu-tms

- URL: https://okestro-edu-team-tms.vercel.app/?mode=edit&access=leader
- 역할: 교육팀 TMS / 팀장 운영 화면
- 상태: 운영 중

### cxr542-ai-portal

- URL: 준비 중
- 역할: 개인/팀 AI 포털
- 상태: 설계/정리 단계

### cxr542-ai-pulse

- URL: 준비 중
- 역할: 알림 / 상태 / 운영 신호 허브
- 상태: 설계/정리 단계

### cxr542-ai-ideabank

- URL: 준비 중
- 역할: 아이디어 / 실험 / 프롬프트 저장소
- 상태: 설계/정리 단계

## Operating Rules

- 운영 데이터 쓰기는 명시 승인 후 수행합니다.
- Blob POST/delete는 승인 없이는 실행하지 않습니다.
- JSON 가져오기는 localStorage 변경 작업이므로 운영에서 신중히 수행합니다.
- push/deploy는 검증 결과를 보고한 뒤 승인받고 진행합니다.
- 실패 가능한 버튼은 운영 UI에서 숨기거나 명확히 안내합니다.

## Deployment Notes

- `cxr542-launcher`는 정적 랜딩 페이지로 운영합니다.
- 실제 서비스 링크만 연결하고, 미구현 앱은 `준비 중`으로 유지합니다.
- 배포 전에는 EDU-TMS 링크와 런처 문구를 먼저 확인합니다.

## Safety Rules

- 운영 데이터에 직접 쓰기 전에 경로와 영향 범위를 확인합니다.
- 백업/복구용 JSON은 수동 절차를 전제로 다룹니다.
- 공유 저장, Blob 반영, 배포는 검증 후 진행합니다.

## iPhone Home Screen

1. iPhone에서 Safari로 https://cxr542-launcher.vercel.app 접속
2. 하단 공유 버튼 선택
3. **홈 화면에 추가** 선택
4. 이름을 `cxr542-ai-workspace` 또는 `AI workspace`로 저장

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

## Related Repos

| Repo | 역할 |
|------|------|
| `edu-team-tms` | 교육팀 TMS |
| `cxr542-portal` | 개인 포털 |
| `cxr542-launcher` | 이 런처 리포지토리 |

TMS에 있던 목업 HTML은 이 repo로 이전되었습니다. TMS `public/preview/` 는 개발 fallback용으로만 유지할 수 있습니다.
