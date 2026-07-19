# HHKB SpaceFN Karabiner Config

HHKB의 `Space` 키를 탭하면 일반 공백으로, 누른 채 다른 키를 조합하면 탐색·편집·미디어·기능 키 레이어로 사용하는 [Karabiner-Elements](https://karabiner-elements.pqrs.org/) Complex Modification 설정입니다.

## 레이어 동작

| 입력 | 동작 |
| --- | --- |
| `Space`를 250ms 이내에 단독으로 탭 | `Space` |
| `Space`를 누른 채 매핑 키 입력 | SpaceFN 레이어의 해당 기능 실행 |
| `Space`에서 손을 뗌 | SpaceFN 레이어 해제 |

> `to_if_alone` 타임아웃이 250ms이므로, `Space`만 250ms보다 오래 누른 뒤 놓으면 공백이 입력되지 않습니다.

## 레이아웃 맵

아래 표기는 `[실제 키 / 출력]`입니다. 표시하지 않은 키는 SpaceFN 레이어에서 별도 매핑이 없습니다.

```text
Space +

    [1/F1] [2/F2] [3/F3] [4/F4] [5/F5] [6/F6] [7/F7] [8/F8] [9/F9] [0/F10] [-/F11] [=/F12]

     Q      W      E      R      T    [Y/PgUp] [U/Home] [I/↑] [O/End]    P
 [A/Vol−] [S/Vol+] [D/Mute] [F/Esc]   G    [H/PgDn] [J/←] [K/↓] [L/→]    ;
     Z      X      C      V      B      N     [M/⌫]   [,/⌦] [./Enter]    /
```

### 최종 매핑

| 조합 | 동작 |
| --- | --- |
| `Space + I/J/K/L` | ↑ / ← / ↓ / → |
| `Space + U/O` | Home / End |
| `Space + Y/H` | Page Up / Page Down |
| `Space + M` | Backspace |
| `Space + ,` | Forward Delete |
| `Space + .` | Enter |
| `Space + F` | Escape |
| `Space + A/S/D` | 볼륨 감소 / 증가 / 음소거 |
| `Space + 1~0` | F1~F10 |
| `Space + -` | F11 |
| `Space + =` | F12 |

## 적용 대상과 구현 방식

- 장치 조건: `vendor_id: 1278` (`0x04FE`), `product_id: 33` (`0x0021`)
- SpaceFN 상태 변수: `hhkb_spacefn`
- 구성: 규칙 1개, manipulator 28개(레이어 제어 1개 + 키 매핑 27개)
- 모든 입력 매핑은 추가 modifier를 허용하도록 `optional: ["any"]`를 사용합니다.
- `Space`를 누르면 `hhkb_spacefn = 1`, 놓으면 `hhkb_spacefn = 0`으로 바뀝니다.
- 키 매핑은 장치 ID가 일치하고 `hhkb_spacefn = 1`일 때만 동작하므로 다른 키보드에는 적용되지 않습니다.

장치가 인식되지 않으면 Karabiner-EventViewer에서 HHKB의 `vendor_id`와 `product_id`를 확인한 뒤 [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json)의 장치 조건을 수정하세요.

## 사용법

`hhkb_spacefn_final.json` 파일을 사용자 홈의 `.config/karabiner/assets/complex_modifications` 폴더에 복사하면 됩니다.

```bash
cp hhkb_spacefn_final.json ~/.config/karabiner/assets/complex_modifications/
```

## 파일

- [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json): Karabiner-Elements에 불러올 원본 설정
- [`README.md`](./README.md): 레이아웃 맵, 설정 분석, 사용법
