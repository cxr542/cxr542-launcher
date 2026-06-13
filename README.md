# cxr542-ai-workspace

`cxr542-launcher`는 `cxr542-ai-workspace` 허브의 정적 진입점입니다.
교육팀 운영, AI 포털, 상태 신호, 아이디어, 프롬프트, 운영 문서를 한 곳에서 묶어 보관합니다.

| 환경 | URL |
|------|-----|
| 운영 | https://cxr542-launcher.vercel.app |
| 로컬 | http://localhost:4321 |

## Purpose

- 팀장과 운영자가 공용 작업 허브로 들어가는 시작점입니다.
- EDU-TMS, AI 포털, 상태 허브, 아이디어 저장소, 런북을 한 화면에서 구분합니다.
- 준비 중인 영역은 실제 링크를 만들지 않고 문서 상태로만 관리합니다.

## Workspace Map

| 영역 | 상태 | 비고 |
|------|------|------|
| okestro-edu-tms | 운영 중 | 팀장 운영 화면 |
| cxr542-ai-portal | 운영 중 | 다음 개선 대상 |
| cxr542-ai-pulse | 준비 중 | 상태 / 알림 / 운영 신호 |
| cxr542-ai-ideabank | 준비 중 | 아이디어 / 실험 / 프롬프트 |
| prompts | 준비 중 | 작업 프롬프트 라이브러리 |
| runbooks | 준비 중 | 운영 / 배포 / 장애 대응 문서 |

## Active Apps

### okestro-edu-tms

- URL: https://okestro-edu-team-tms.vercel.app/?mode=edit&access=leader
- 역할: 교육팀 운영, KPI, 업무일지, 향상 과제, 장부 관리 시스템
- 상태: 운영 중

### cxr542-ai-portal

- URL: https://cxr542-portal.vercel.app/
- 역할: 개인/팀 AI 포털
- 상태: 운영 중, 다음 개선 대상

## Planned Apps

### cxr542-ai-pulse

- URL: 준비 중
- 역할: 상태, 알림, 운영 신호, 체크리스트 허브
- 상태: 준비 중

### cxr542-ai-ideabank

- URL: 준비 중
- 역할: 아이디어, 프롬프트, 실험 후보 저장소
- 상태: 준비 중

## Workspace Assets

### prompts

- 상태: 준비 중
- 역할: Codex/Cursor 작업 프롬프트 라이브러리

### runbooks

- 상태: 준비 중
- 역할: 배포, 운영, 장애 대응 절차 문서

### n8n PoC

- 상태: 초안
- 역할: GitHub Actions 실패와 Vercel 배포 상태를 분류하는 read-only 자동화 실험
- 문서: `docs/n8n/github-actions-vercel-deploy-classifier.md`

## Operating Rules

- 운영 데이터 쓰기는 명시 승인 후 수행합니다.
- Blob POST/delete는 승인 없이 실행하지 않습니다.
- JSON 가져오기는 localStorage 변경 작업이므로 운영에서 신중히 수행합니다.
- push/deploy는 검증 결과 보고 후 승인받고 진행합니다.
- 실패 가능한 버튼은 운영 UI에서 숨기거나 명확히 안내합니다.

## Safety Rules

- 운영 데이터에 직접 쓰기 전에 경로와 영향 범위를 확인합니다.
- 백업/복구용 JSON은 수동 절차를 전제로 다룹니다.
- 공유 저장, Blob 반영, 배포는 검증 후 진행합니다.
- 준비 중인 앱은 실제 링크가 없으면 활성 링크로 만들지 않습니다.

## Next Priorities

1. `cxr542-ai-portal`의 다음 개선 범위를 정리합니다.
2. `cxr542-ai-pulse`와 `cxr542-ai-ideabank`의 문서 골격을 마련합니다.
3. prompts / runbooks 디렉터리 구조를 정리합니다.

## iPhone Home Screen

1. iPhone에서 Safari로 https://cxr542-launcher.vercel.app 접속
2. 하단 공유 버튼 선택
3. **홈 화면에 추가** 선택
4. 이름을 `cxr542-ai-workspace` 또는 `AI workspace`로 저장

## Development

```bash
npm run dev
```

TMS·Portal에서 `← Workspace` 링크는 운영 시 위 URL을 사용합니다.  
로컬 개발 시 각 앱에 `VITE_LAUNCHER_ORIGIN=http://localhost:4321` (선택).

## Deployment

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
