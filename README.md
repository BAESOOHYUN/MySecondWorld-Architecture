# MySecondWorld — 시스템 아키텍처 도면

[MySecondWorld](https://github.com/BAESOOHYUN/MySecondWorld) (Unity 6 기반 서버 권위 3D 멀티플레이어 액션 RPG, 1인 개발)의 **전 계층 시스템 아키텍처 도면 저장소**입니다.  
네트워크, 차세대 AI NPC, 전투, 렌더링, 인프라 자동화까지 1인 개발로 구축한 전체 15개 도메인의 구조도가 `architecture.drawio` 단일 파일에 수록되어 있습니다.

> 📐 **[웹 뷰어로 도면 15장 바로 보기 (클릭)](https://viewer.diagrams.net/?lightbox=1&nav=1&layers=1&title=MySecondWorld#Uhttps%3A%2F%2Fraw.githubusercontent.com%2FBAESOOHYUN%2FMySecondWorld-Architecture%2Fmain%2Farchitecture.drawio)**  
> *(링크 접속 후 하단 중앙의 `‹` `›` 버튼을 통해 1장부터 15장까지 순서대로 넘겨보실 수 있습니다.)*

---

## 🔗 핵심 프로젝트 링크

| 구분 | 링크 |
|---|---|
| 📄 **포트폴리오 기술 명세서 (Notion)** | [MySecondWorld 포트폴리오 기술 문서](https://app.notion.com/p/MySecondWorld-3D-RPG-419c12defa4981838af7d853933281a5) |
| 💻 **게임 메인 저장소 (GitHub)** | [BAESOOHYUN/MySecondWorld](https://github.com/BAESOOHYUN/MySecondWorld) |
| 🎬 **시연 및 개발 영상 (YouTube)** | [YouTube 시연 플레이리스트 바로가기](https://youtube.com/playlist?list=PLbzoJ0fZJVF8&si=ITH6kSl-xUE1n3N-) |

---

## 🏆 핵심 기술 5건과 아키텍처 도면

각 도면은 포트폴리오 기술 문서의 문제 분석, 원인 규명, 해결 코드와 1:1로 연결되어 있습니다.

| 핵심 기술 주제 | 관련 도면 | 아키텍처 해결 요약 |
|---|---|---|
| **심리스 4인 룸 인스턴싱 & 공간 분할**<br>*(마비노기 '우연한 만남' 모티브)* | **5장** | Unity의 동일 씬 Additive 로드 한계를 극복하기 위해 `matchId(Guid)` 기반 `MatchInterestManagement`로 공간 분할 트래픽 O(1) 격리. 유령 몬스터 피격 버그는 전용 통보 메시지 신설 및 스폰 오브젝트 소속 씬 이전으로 해결. |
| **0.9초 음성 파이프라인 & 서버 영속 기억 AI NPC** | **6장, 14장** | STT → LLM 스트리밍 → 문장 슬라이싱 & TTS 비동기 프리페치 큐 → 256샘플 진폭 RMS 립싱크 (첫 소리 중앙값 약 0.9초 실측). C++ P/Invoke `0xC0000005` 크래시 방어 및 10쌍 기억의 서버 세이브 영속화. |
| **기획·아트를 위한 4축 모듈러 스킬 시스템** | **7장** | Trigger · Targeting · Effect · Sequence를 Strategy + Composite 패턴으로 직교 분리하여 SO 조합만으로 스킬을 저작하는 노코드 환경 구축. 서버 SphereCast 스윕 판정 독점 및 클라이언트 비동기 타임라인 연출. |
| **552개 모듈러 파츠 동기화 & 0ms 클라이언트 예측** | **9장, 15장** | 외형 원본(SSOT)을 서버 세이브로 일원화하고 네트워크 RTT 지연을 상쇄하는 0ms 클라이언트 예측 렌더링. 데디서버 DI 누락 원인 규명 및 슬롯 번호 기반 신원 체계/타임스탬프로 연타 깜빡임 버그 방어. |
| **12KB 청크 스트리밍 & 실시간 대화면 파일 공유** | **11장** | Mirror 64KB 패킷 한계 크래시를 12,000바이트 청크 슬라이싱으로 극복. Outer Zone 관심 영역(AOI) 분할로 불필요한 트래픽을 차단하고 지각 입장자(Late-Joiner)를 위한 서버 캐시 동기화 구현. |

---

## 📑 전체 도면 목차 (15개 장)

| 장 | 도면 명칭 | 주요 아키텍처 및 엔지니어링 내용 |
|:---:|---|---|
| **1** | **전체 구조** | Presentation, Architecture, Network, Dedicated Server 4-Tier 전 계층 엔드-투-엔드(E2E) 시스템 구성도 |
| **2** | **DI 스코프 계층** | VContainer 계층형 스코프(`ProjectLifetimeScope` → `NPCLifetimeScope` → `NPCScope`) 및 서버/클라이언트 객체 오염 방지 |
| **3** | **어셈블리 구조** | 18개 런타임 `.asmdef` 도메인 분리 및 상위에서 하위로만 흐르는 단방향 의존성 규칙 |
| **4** | **어셈블리 순환 해결** | 중립 인터페이스 레이어(`Foundation`)를 통한 도메인 모듈 간 순환 참조(Circular Dependency) 원천 차단 |
| **5** | **네트워크 · 접속 · 존 · 던전 방** | Mirror 기반 네트워크 루프, AWS EC2 헤드리스 서버, `MatchInterestManagement` 4인 룸 트래픽 격리 파이프라인 |
| **6** | **AI NPC 파이프라인** | 마이크 캡처(STT) → LLM 스트리밍 → 문장 슬라이싱 & TTS 프리페치 큐 → 진폭 기반 립싱크 비동기 파이프라인 |
| **7** | **전투 · 스킬 시스템** | 4축 직교 분리(Strategy/Composite), UI Toolkit 기반 비주얼 스킬 에디터, 서버 SphereCast 권위 판정 흐름 |
| **8** | **몬스터 AI · 웨이브 · 컴패니언** | Stateless 기반 몬스터 상태 머신, NavMesh 경로 추적, 플레이어 추종 및 자동 전투 컴패니언 AI 로직 |
| **9** | **인벤토리 · 장비 · 파츠 장착** | 552개 모듈러 파츠 본 리매핑, 무기 소켓 장착 파이프라인, 서버 세이브 데이터베이스 복원 구조 |
| **10** | **입력 · 카메라 · UI · 씬 안전장치** | New Input System 터치/키보드 이벤트 분기, Cinemachine 3 OrbitalFollow 제어, 포탈 전환 시 씬 겹침 방지 대피 가드 |
| **11** | **쉐어드 스크린 · 파일 전송 · 동기화** | 12KB 청크 분할 스트리밍, Outer Zone AOI 트래픽 최적화, PDF 렌더링 텍스처 셰어링 |
| **12** | **렌더링 최적화 · 오브젝트 풀링** | URP 모바일 렌더링 파이프라인, 메시 LOD/HLOD, SpriteAtlas, 제네릭 오브젝트 풀링 구조 |
| **13** | **빌드 · 배포 파이프라인** | 에디터 원클릭 리눅스 데디서버 빌드, SCP/SSH 전송, AWS EC2 systemd 데몬 자동 재시작 및 배포 자동화 |
| **14** | **AI NPC 기억 · 상점 — 클라와 서버** | 10쌍 대화 기억 캐시(`NPCMemorySO`) 및 서버 세이브 영속화, 맥락 기반 상점 추천 및 서버 거래 검증 |
| **15** | **외형 동기화 — 서버 원본 · 칸 번호 · 낡은 응답 무시** | 0ms 클라이언트 예측 렌더링, 인벤토리 슬롯 번호 기반 파츠 추적, 타임스탬프 필터링을 통한 역행 방어 |

---

## 🛠️ 도면 직접 열람 및 편집 안내

- **웹 브라우저 열람:** 상단의 **[웹 뷰어 링크](https://viewer.diagrams.net/?lightbox=1&nav=1&layers=1&title=MySecondWorld#Uhttps%3A%2F%2Fraw.githubusercontent.com%2FBAESOOHYUN%2FMySecondWorld-Architecture%2Fmain%2Farchitecture.drawio)**를 클릭하시면 별도 프로그램 설치 없이 고해상도로 확대/축소 및 페이지 탐색이 가능합니다.
- **로컬 원본 편집:** 저장소 루트의 `architecture.drawio` 파일을 다운로드하여 [draw.io (app.diagrams.net)](https://app.diagrams.net) 웹 또는 데스크톱 애플리케이션에서 열면 모든 레이어와 벡터 요소를 직접 수정하실 수 있습니다.

---

## 👤 Author

**배수현 (Bae Soohyun)**  
- Role: Game Programmer (Client / Server)  
- Contact: bsh9277@naver.com  
- Portfolio: [Notion 포트폴리오 바로가기](https://app.notion.com/p/MySecondWorld-3D-RPG-419c12defa4981838af7d853933281a5)
