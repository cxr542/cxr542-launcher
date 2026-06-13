# n8n PoC 1 — GitHub Actions 실패와 Vercel 배포 상태 분류

## Purpose

GitHub Actions의 `Deploy Production` 워크플로우가 실패했을 때, Vercel의 최신 production deployment 상태를 read-only로 조회해 실제 운영 장애인지, Actions 워크플로우만 실패했는지 분류합니다.

## Problem

`cxr542/cxr542-launcher`에서 `Run failed: Deploy Production - main (cd539be)` 알림이 발생했지만, Vercel의 최신 production deployment는 `READY`였습니다.

이 경우 실제 서비스 배포는 정상이고 GitHub Actions workflow만 실패했을 가능성이 높습니다. 수동 확인 없이도 이 차이를 분류하는 보조 절차가 필요합니다.

## Scope

- GitHub Actions 실패 알림을 입력으로 받습니다.
- Vercel latest production deployment를 조회합니다.
- 상태와 commit SHA를 비교해 분류합니다.
- 요약 메시지를 생성해 알림 채널로 전달합니다.

## Non-goals

- GitHub Actions rerun
- Vercel redeploy
- rollback
- GitHub issue/comment 생성
- 운영 데이터 쓰기
- Blob POST/delete
- 외부 입력을 명령으로 실행하는 동작

## Workflow Overview

1. Manual Trigger 또는 Webhook Trigger로 시작합니다.
2. 실패한 GitHub Actions 정보와 commit SHA를 입력받습니다.
3. Vercel latest production deployment를 조회합니다.
4. deployment state, target, commit SHA를 확인합니다.
5. 분류 규칙에 따라 상태를 결정합니다.
6. 요약 메시지를 생성합니다.
7. 알림 채널로 전달합니다.

## Inputs

- `repo`: `cxr542/cxr542-launcher`
- `branch`: `main`
- `failed workflow name`: `Deploy Production`
- `commit sha`: short SHA 또는 full SHA
- `failed run url`: optional

## Vercel Check Logic

조회 대상은 최신 production deployment입니다.

- project: `cxr542-launcher`
- target: `production`
- 확인 항목:
  - `state`
  - `commit sha`
  - `message`
  - `target`
  - `createdAt`

## Classification Rules

### Case A

- GitHub Actions failed
- Vercel latest production deployment is `READY`
- latest deployment commit matches failed commit 또는 더 최신

결론: 운영 장애 아님. Actions workflow만 실패했을 가능성이 높습니다.

### Case B

- GitHub Actions failed
- Vercel latest production deployment is `ERROR`, `FAILED`, 또는 `CANCELED`

결론: 실제 배포 실패 가능성이 높습니다. 로그 확인이 필요합니다.

### Case C

- GitHub Actions failed
- 최근 Vercel production deployment가 없음

결론: 배포 트리거 누락 또는 Vercel Git Integration 문제 가능성이 있습니다.

### Case D

- GitHub Actions failed
- Vercel latest deployment is `READY`
- 하지만 해당 commit이 failed commit보다 오래됨

결론: 최신 커밋이 production에 반영되지 않았을 수 있습니다. 추가 확인이 필요합니다.

## Notification Drafts

### Workflow only failure

`GitHub Actions Deploy Production failed, but Vercel production is READY for the latest commit. This looks like a workflow-only failure.`

### Real deployment failure

`GitHub Actions Deploy Production failed and Vercel production deployment is ERROR/FAILED/CANCELED. This likely needs deployment log inspection.`

### Missing deployment

`GitHub Actions Deploy Production failed, but no recent Vercel production deployment was found. Check the deployment trigger and Vercel integration.`

### Stale READY deployment

`GitHub Actions Deploy Production failed, and Vercel production is READY on an older commit. The latest commit may not have reached production.`

## Required Secrets

Placeholder only. 실제 값은 저장하지 않습니다.

- `VERCEL_TOKEN`
- `VERCEL_TEAM_ID`
- `VERCEL_PROJECT_ID_CXR542_LAUNCHER`
- `NOTIFY_WEBHOOK_URL`
- or `TELEGRAM_BOT_TOKEN`
- or `TELEGRAM_CHAT_ID`

## Safety Rules

- read-only 확인만 수행합니다.
- GitHub Actions rerun 금지
- Vercel redeploy 금지
- rollback 금지
- GitHub issue/comment 생성 금지
- 운영 데이터 쓰기 금지
- Blob POST/delete 금지
- 외부 입력을 명령으로 실행하지 않습니다.

## Manual Test Plan

1. Manual Trigger로 샘플 input을 넣습니다.
2. Vercel latest production deployment 조회 결과를 확인합니다.
3. `READY` + 최신 commit 일치 케이스를 분류합니다.
4. `FAILED` 케이스를 분류합니다.
5. deployment 없음 케이스를 분류합니다.
6. 알림 문구가 과도하게 단정적이지 않은지 확인합니다.

## Next Steps

- 실제 n8n import를 하지 않고 워크플로우 구조만 유지합니다.
- GitHub Actions 실패 이벤트 포맷을 더 구체화할 수 있습니다.
- 알림 채널별 메시지 템플릿을 분리할 수 있습니다.
