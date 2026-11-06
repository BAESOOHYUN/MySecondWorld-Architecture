# MySecondWorld — 아키텍처 도면

[MySecondWorld](https://github.com/BAESOOHYUN/MySecondWorld)(Unity 6 기반 크로스플랫폼 멀티플레이어 액션 RPG, 1인 개발)의 아키텍처 도면 저장소입니다. 도면 13장이 `architecture.drawio` 한 파일에 들어 있습니다.

## 👉 [도면 바로 보기](https://viewer.diagrams.net/?lightbox=1&nav=1&layers=1&title=MySecondWorld#Uhttps%3A%2F%2Fraw.githubusercontent.com%2FBAESOOHYUN%2FMySecondWorld-Architecture%2Fmain%2Farchitecture.drawio)

화면 아래 ‹ › 버튼(마우스를 올리면 보입니다)으로 장을 넘기고, 확대해서 자세히 볼 수 있습니다. 파일을 고치면 이 링크에는 몇 분 뒤 반영됩니다.

## 도면 목록

| 장 | 내용 |
|---|---|
| 1 | 전체 구조 |
| 2 | DI 스코프 구조 (VContainer) |
| 3 | 어셈블리(asmdef) 분리 — 참조는 위에서 아래로만 |
| 4 | 어셈블리 순환 참조 해결 |
| 5 | 네트워크 (Mirror, 관심 영역 관리) |
| 6 | AI NPC 파이프라인 (STT → LLM → TTS → 립싱크) |
| 7 | 전투 · 스킬 시스템 |
| 8 | 몬스터 · 컴패니언 AI |
| 9 | 인벤토리 · 장비 · 서버 저장 |
| 10 | 입력 · 카메라 · UI |
| 11 | 쉐어드 스크린 (파일 공유) |
| 12 | 렌더링 최적화 · 오브젝트 풀링 |
| 13 | 빌드 · 배포 파이프라인 |

## 함께 보기

- 📄 [기술 문서 (Notion)](https://scythe-lavender-093.notion.site/2026-3d4c12defa4980f994a8da0cf10573a0) — 문제 → 원인 → 해결 → 검증 과정
- 💻 [프로젝트 저장소](https://github.com/BAESOOHYUN/MySecondWorld)
- 🎥 [플레이 영상](https://youtube.com/playlist?list=PLbzoJ0fZJVF8&si=b4vfPgADLcIZXj6A)

## 파일을 직접 열려면

`architecture.drawio`를 내려받아 [draw.io](https://app.diagrams.net)에서 열면 편집 가능한 원본을 볼 수 있습니다.

---

**배수현 (Bae Soohyun)** — Unity 게임 프로그래머 (클라이언트 / 서버)
