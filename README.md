# 산업안전사고 가상체험 4DX — v2.2

## 변경 사항: 사고 종료 후 경고 이미지

세 장면 모두 **사고 동작이 끝난 다음에만** `safety-accident-alert.png`가 나타납니다. 경고 이미지는 약 **2.2초**간 표시된 후 사라집니다. 사고 동작 중에는 나타나지 않습니다.

1. **① 개구부 추락**: 작업자가 개구부로 이동해 아래로 추락하고 사라진 뒤, 지정된 추락 지점(화면 기준 x=47.85%, y=68.15%)에 경고 이미지를 표시합니다.
2. **② 지게차 충돌**: 지게차가 지정 위치로 후진해 충돌하고, 작업자가 바닥으로 쓰러지는 동작을 마친 뒤, 작업자 위치에 경고 이미지를 표시합니다.
3. **③ 전기설비 감전**: 작업자가 설비 쪽으로 이동해 감전되고, 바닥으로 쓰러지는 동작을 마친 뒤, 작업자 위치에 경고 이미지를 표시합니다.

사고 전의 기존 이동·회전·충돌·추락·쓰러짐 로직은 변경하지 않았습니다. **작업자의 전기설비 방향은 기본 180° + 회전 116° = 296°**를 유지합니다. 메뉴는 위 세 장면만 유지합니다.

## GitHub 파일 구조

```text
industrial-safety-4dx/
├── index.html
├── README.md
└── assets/
    ├── construction_worker.glb
    ├── forklift.glb
    ├── electrical-box.glb
    ├── backgrounds/
    │   ├── gaegubu.png
    │   ├── jigecha.png
    │   └── gamjeon.png
    └── effects/
        └── safety-accident-alert.png
```

`assets/effects/safety-accident-alert.png`는 **대소문자와 하이픈까지 정확하게** 일치해야 합니다. 이미지 파일은 사용자가 GitHub에 별도로 업로드해야 합니다. 이미지가 투명 배경이 아닌 경우 이미지의 사각형 배경도 함께 보입니다. 투명 PNG를 사용하면 현장 화면에 자연스럽게 겹쳐집니다.

## 설치 방법

1. `industrial_safety_v2_2_index.html`을 `index.html`로 이름을 바꿔 저장소 루트의 기존 파일을 교체합니다.
2. `industrial_safety_v2_2_README.md`를 `README.md`로 이름을 바꿔 교체합니다.
3. 경고 이미지를 `assets/effects/safety-accident-alert.png`로 업로드합니다.
4. GitHub Pages를 열고 `Ctrl + F5`로 새로고침한 뒤, 세 장면의 사고 **완료 이후**에 경고가 나타나는지 확인합니다.

## 기술 메모

- 사고 후 경고 이미지는 HTML의 `img#accidentAlert` 오버레이로 구현합니다.
- 표시 시점: `impact` 상태에서 약 1.9초간 추락/쓰러짐 처리 → `alert` 상태에서 이미지 2.2초 표시 → `done` 상태로 종료.
- 장면 초기화·긴급 정지·장면 전환 시 경고 이미지를 숨깁니다.
- 실제 GitHub Pages에서 GLB와 경고 PNG를 함께 로딩한 시각적 테스트는 수행하지 못했습니다.
