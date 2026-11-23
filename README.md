# 산업안전사고 가상체험 4DX

**실제 산업현장 배경 이미지 + GLB 3D 모델**을 조합하여 다섯 가지 산업안전사고의 위험을 체험하는 교육용 웹 콘텐츠입니다.

## 체험 내용

| 순서 | 사고 유형 | 배경 이미지 | 핵심 3D 모델 |
|---|---|---|---|
| 1 | 건설현장 개구부 추락 | `gaegubu.png` | `construction_worker.glb` |
| 2 | 선반작업 끼임 | `seonban.png` | `lathe.glb`, `lathe_chuck.glb`, `construction_worker.glb` |
| 3 | 지게차 충돌 | `jigecha.png` | `forklift.glb`, `construction_worker.glb` |
| 4 | 전기설비 감전 | `gamjeon.png` | `electrical-box.glb`, `construction_worker.glb` |
| 5 | 밀폐공간 질식 | `jilsik.png` | `storage-tanks.glb`, `construction_worker.glb` |

## GitHub 폴더 구조

```text
industrial-safety-4dx/
├── index.html
├── README.md
└── assets/
    ├── construction_worker.glb
    ├── lathe.glb
    ├── lathe_chuck.glb
    ├── forklift.glb
    ├── electrical-box.glb
    ├── storage-tanks.glb
    └── backgrounds/
        ├── gaegubu.png
        ├── seonban.png
        ├── jigecha.png
        ├── gamjeon.png
        └── jilsik.png
```

> GitHub는 대소문자를 구분합니다. 파일명을 위와 정확히 일치시키세요.

## 사용법

1. 왼쪽에서 사고 현장을 선택합니다.
2. 현장 사진과 GLB 모델이 로딩되면 **사고 시뮬레이션 시작**을 누릅니다.
3. 위험 행동과 안전 행동을 선택해 교육 메시지를 확인합니다.
4. **안전조치 확인**으로 예방수칙을 복습합니다.
5. GLB가 배경과 어긋나 보이면 왼쪽의 **좌우·상하·크기·회전** 조절기를 사용합니다. 조절기는 해당 장면의 주 설비에 적용되며 저장되지 않습니다.

## GitHub Pages 게시

1. 저장소 루트에 `index.html`, `README.md`를 업로드합니다.
2. `assets`에 GLB 6개, `assets/backgrounds`에 PNG 5개를 업로드합니다.
3. **Settings → Pages → Build and deployment → Deploy from a branch**에서 `main` 및 `/(root)`를 선택합니다.
4. 배포가 완료되면 `https://imm-content.github.io/industrial-safety-4dx/`로 접속합니다(저장소 소유자가 `imm-content`인 경우).

Three.js는 jsDelivr CDN을 사용하므로 인터넷 연결이 필요합니다. HTML을 파일 탐색기에서 직접 여는 `file://` 방식은 GLB 로딩이 차단될 수 있습니다. GitHub Pages나 로컬 웹 서버에서 실행하세요.

## 구현 범위와 한계 (v0.2)

- **구현:** 사진 배경 5개 연동, GLB 모델 6개 연동, 카메라에 투영된 3D 모델, 장면별 모델 이동, 선반 척 회전, 지게차 후진 이동, 경고음, 화면 흔들림, 음성 안내, 선택형 예방교육.
- **한계:** 배경은 2D 사진입니다. 사진 속 구조물과 GLB 사이에는 실제 3D 깊이·가림·충돌 판정이 없습니다. 개구부 아래층, 선반의 정확한 회전축, 지게차 바퀴의 개별 회전, 작업자 보행·손 동작, 배전반 접촉, 탱크 내부 진입은 완전한 물리/인체 애니메이션이 아닙니다. 일부는 카메라·위치·시각 효과로 근사합니다.
- **모델 정렬:** GLB마다 축·크기·중심이 달라 현장 사진과의 위치/원근 정렬은 실제 실행 화면을 기준으로 추가 보정이 필요합니다. 선반 척은 별도 모델로 겹쳐 표시하므로 원본 선반의 척과 중첩될 수 있습니다.
- **기기 효과:** 일반 브라우저에서 실제 4DX 좌석, 바람, 물 분사 효과는 지원하지 않습니다. 진동은 지원되는 기기에서만 작동합니다.

## 안전 및 저작권

이 콘텐츠는 산업안전 교육용 가상 시뮬레이션으로, 실제 사고 재현의 정확성을 보증하지 않으며 법정 안전교육이나 현장 안전작업 절차를 대체하지 않습니다. 감전·밀폐공간 등 고위험 작업은 자격·작업허가·현장 절차에 따라 수행해야 합니다.

외부에서 받은 GLB의 저작권과 라이선스(예: CC BY)를 확인하고 모델별 제작자·출처 URL·라이선스를 기록하세요. 배경 이미지 역시 공개·상업적 사용 권한을 확인하세요.

## 향후 개선

- GLB별 축 방향과 접지점 정밀 보정
- 작업자 리깅 및 걷기/손 동작 애니메이션
- 선반 원본 척 제거 후 회전 척 정확히 장착
- 지게차 바퀴 분리·회전 및 실제 주행축 검증
- 사진 배경을 3D 공간으로 단계적 대체하여 진짜 추락/탱크 진입 구현


## v0.3 실행 오류 수정
- Three.js `GLTFLoader`가 내부적으로 사용하는 `three` 모듈 경로를 import map으로 지정했습니다. 기존 버전에서 메뉴가 비고 '준비 중'에 멈추는 원인이 될 수 있는 모듈 해석 오류를 수정했습니다.
- 체험 화면을 브라우저 가로 폭에 맞춰 확대하고, **체험 화면 전체화면** 버튼을 추가했습니다.
- GitHub Pages에 `index.html`을 덮어쓴 후 **Ctrl+F5**로 새로고침하세요.
- 여전히 실행되지 않으면 F12 → Console의 첫 번째 빨간 오류 메시지를 확인해 주세요.
- 배경은 2D 사진이므로 GLB 모델과 사진 속 물체 사이의 실제 3D 가림·충돌은 아직 구현되지 않았습니다.
