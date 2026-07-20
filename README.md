# HHKB Safe-Hold SpaceFN Karabiner Config

HHKB의 `Space`를 짧게 누르면 일반 공백으로, 의도적으로 75ms 이상 누르면 탐색·편집·기호·미디어·기능 키 레이어로 사용하는 [Karabiner-Elements](https://karabiner-elements.pqrs.org/) Complex Modification 설정입니다.

빠른 타이핑에서 `Space`를 떼기 전에 다음 글자를 누르더라도 공백과 글자를 모두 보존하도록 롤오버 안전 처리를 포함합니다.

## Space 판정 방식

| 입력 | 동작 |
| --- | --- |
| `Space`를 500ms 이내에 단독으로 탭 | `Space` |
| `Space`를 누른 뒤 75ms 이내에 다른 키 입력 | 일반 `Space + 해당 키` 입력 |
| `Space`를 75ms 이상 홀드 | SpaceFN 레이어 활성화 |
| 활성화 후 매핑 키 입력 | SpaceFN 레이어 기능 실행 |
| `Space`에서 손을 뗌 | SpaceFN 레이어 해제 |

예를 들어 75ms 이내에 `Space → A/S/D`를 겹쳐 입력하면 음량 기능이 아니라 `공백 + A/S/D`가 정상 입력됩니다. 75ms 이상 Space를 홀드한 뒤 A/S/D를 누르면 볼륨 감소·증가·음소거가 실행됩니다.

> `Space`만 500ms 이상 누른 뒤 놓으면 공백이 입력되지 않습니다. SpaceFN 조합은 먼저 `Space`를 약 75ms 홀드한 뒤 대상 키를 누르세요.

## 레이아웃 맵

아래 표기는 `[실제 키 / 출력]`입니다. 표시하지 않은 키는 SpaceFN 레이어에서 별도 매핑이 없습니다.

```text
Space 75ms hold +

    [1/F1] [2/F2] [3/F3] [4/F4] [5/F5] [6/F6] [7/F7] [8/F8] [9/F9] [0/F10] [-/F11] [=/F12]

       Q     [W/[]  [E/]]  [R/']  [T//] [Y/PgUp] [U/Home] [I/↑] [O/End]    P
 [A/Vol−] [S/Vol+] [D/Mute] [F/Esc] [G/;] [H/PgDn] [J/←] [K/↓] [L/→]    ;
       Z     [X/−]   [C/=]  [V/\] [B/`·₩] [N/?]   [M/⌫]   [,/⌦] [./Enter]  /
```

### 탐색 및 편집

| 조합 | 동작 |
| --- | --- |
| `Space + I/J/K/L` | ↑ / ← / ↓ / → |
| `Space + U/O` | Home / End |
| `Space + Y/H` | Page Up / Page Down |
| `Space + M` | Backspace |
| `Space + ,` | Forward Delete |
| `Space + .` | Enter |
| `Space + F` | Escape |

### 기호

| 조합 | 출력 | Shift를 먼저 누른 조합 |
| --- | --- | --- |
| `Space + W/E` | `[` / `]` | `{` / `}` |
| `Space + R` | `'` | `"` |
| `Space + T` | `/` | `?` |
| `Space + G` | `;` | `:` |
| `Space + X` | `-` | `_` |
| `Space + C` | `=` | `+` |
| `Space + V` | `\` | `|` |
| `Space + B` | ABC에서는 `` ` ``, 두벌식에서는 `₩` | 입력 소스에 따라 `~` 등 |
| `Space + N` | `?` | — |

Shift 기호는 `Shift`를 먼저 누른 상태에서 `Space`를 75ms 홀드한 뒤 대상 키를 누르는 순서가 가장 안정적입니다.

### 미디어 및 기능 키

| 조합 | 동작 |
| --- | --- |
| `Space + A/S/D` | 볼륨 감소 / 증가 / 음소거 |
| `Space + 1~0` | F1~F10 |
| `Space + -` | F11 |
| `Space + =` | F12 |

일반 타이핑으로 A/S/D를 입력하려면 Space를 75ms 이내에 다음 키와 겹쳐 누르고, 미디어 기능을 사용하려면 Space를 75ms 이상 홀드한 뒤 A/S/D를 누르세요.

## 타이밍 조정

[`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json)의 다음 두 값은 항상 같은 값으로 유지해야 합니다.

```json
"basic.to_if_held_down_threshold_milliseconds": 75,
"basic.to_delayed_action_delay_milliseconds": 75
```

- 일반 타이핑에서 레이어가 여전히 실수로 켜지면 두 값을 함께 `100` 또는 `120`으로 올립니다.
- SpaceFN이 너무 늦게 켜지면 두 값을 함께 `50`으로 내립니다.
- 단독 Space 허용 시간은 `basic.to_if_alone_timeout_milliseconds: 500`입니다.

## 적용 대상과 구현 방식

- 장치 조건: `vendor_id: 1278` (`0x04FE`), `product_id: 33` (`0x0021`)
- SpaceFN 상태 변수: `hhkb_spacefn`
- 구성: 규칙 1개, manipulator 38개(레이어 제어 1개 + 기능·기호 37개)
- `Space`를 75ms 홀드하면 `hhkb_spacefn = 1`, 놓으면 `key_up_value`로 `0`이 됩니다.
- 75ms 이전의 다른 키 입력은 `to_delayed_action.to_if_canceled`가 먼저 공백을 복원합니다.
- 일반 레이어 매핑은 추가 modifier를 보존하므로 Shift 기호와 탐색 modifier를 사용할 수 있습니다.
- 키 매핑은 장치 ID가 일치하고 `hhkb_spacefn = 1`일 때만 동작하므로 다른 키보드에는 적용되지 않습니다.

`key_up_value`를 사용하므로 Karabiner-Elements 14.12.6 이상이 필요합니다.

장치가 인식되지 않으면 Karabiner-EventViewer에서 HHKB의 `vendor_id`와 `product_id`를 확인한 뒤 [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json)의 장치 조건을 수정하세요.

## 사용법

`hhkb_spacefn_final.json` 파일을 사용자 홈의 `.config/karabiner/assets/complex_modifications` 폴더에 복사한 뒤 Karabiner-Elements에서 규칙을 추가하면 됩니다.

```bash
cp hhkb_spacefn_final.json ~/.config/karabiner/assets/complex_modifications/
```

## 파일

- [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json): Karabiner-Elements에 불러올 설정
- [`README.md`](./README.md): 레이아웃, 안전한 Space 판정 방식, 타이밍 조정법
