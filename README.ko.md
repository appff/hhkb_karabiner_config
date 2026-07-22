# 60% Ergo

60% Ergo는 60% 이하 배열을 위한 인체공학적 SpaceFN 키맵입니다. 새끼손가락의 부담과 오른쪽 손목이 바깥쪽으로 꺾이는 동작을 줄이고, 익숙한 컴팩트 키보드 사용 경험은 유지하면서 장시간 코딩을 더 편안하게 만드는 것이 목표입니다.

> Don't adapt your hands to the keyboard. Adapt the keyboard to your hands.
>
> 손을 키보드에 맞추지 말고, 키보드를 손에 맞추세요.

[English README](./README.md)

60% Ergo는 오른손 새끼손가락을 반복적으로 뻗고 오른쪽 손목이 바깥쪽으로 꺾이는 동작 때문에 생기는 부담과 피로를 줄이기 위해 만들었습니다. 자주 사용하는 탐색·편집·기호·미디어·기능 키를 왼쪽 엄지로 누르는 SpaceFN 레이어에 배치해 오른손의 이동과 부담을 줄이는 것이 목표입니다.

이 [Karabiner-Elements](https://karabiner-elements.pqrs.org/) Complex Modification은 이 컴퓨터에 연결된 모든 키보드의 `Space`를 다음 두 가지 방식으로 사용합니다.

- `Space`를 짧게 누르면 일반 공백
- `Space`를 50ms 이상 홀드하면 SpaceFN 레이어 활성화

빠른 타이핑에서 `Space`를 떼기 전에 다음 글자를 누르는 경우에도 공백과 다음 키를 보존하도록 롤오버 안전 처리를 포함합니다.

## Space 판정 방식

| 입력 | 동작 |
| --- | --- |
| `Space`를 500ms 이내에 단독으로 탭 | 일반 `Space` |
| `Space`를 누른 뒤 50ms 이내에 다른 키 입력 | 일반 `Space + 해당 키` 입력 |
| `Space`를 50ms 이상 홀드 | SpaceFN 레이어 활성화 |
| 레이어 활성화 후 매핑 키 입력 | SpaceFN 기능 실행 |
| `Space`에서 손을 뗌 | SpaceFN 레이어 해제 |
| `Ctrl + Space` | SpaceFN을 거치지 않고 macOS 입력 소스 전환으로 전달 |

대상 키가 50ms보다 먼저 입력되면 해당 SpaceFN 시도는 취소되고 지연 동작이 일반 공백을 복원합니다. SpaceFN 조합은 `Space`를 먼저 누르고 잠깐 유지한 뒤 대상 키를 누르는 순서가 안정적입니다.

> `Space`만 500ms 이상 누른 뒤 놓으면 공백이 입력되지 않습니다. SpaceFN 조합은 `Space`를 약 50ms 홀드한 뒤 대상 키를 누르세요.

## 레이아웃 맵

아래 표는 모든 SpaceFN 매핑을 `[실제 키 / 출력]` 기준으로 정리한 것입니다. 표에 없는 키는 SpaceFN에서 별도 매핑이 없습니다.

| 실제 키 | SpaceFN 출력 | 용도 |
| --- | --- | --- |
| `1`–`0` | `F1`–`F10` | 기능 키 |
| `-` / `=` | `F11` / `F12` | 기능 키 |
| `W` / `E` | `[` / `]` | 대괄호 |
| `R` / `T` | `'` / `/` | 따옴표·슬래시 |
| `Y` / `H` | Page Up / Page Down | 페이지 이동 |
| `U` / `O` | Home / End | 줄 이동 |
| `I` / `J` / `K` / `L` | ↑ / ← / ↓ / → | 커서 이동 |
| `A` / `S` / `D` | 볼륨 감소 / 볼륨 증가 / 음소거 | 미디어 |
| `F` | Escape | 편집 |
| `G` | `;` | 기호 |
| `M` | Backspace | 편집 |
| `,` | Forward Delete | 편집 |
| `.` | Enter | 편집 |
| `X` / `C` | `-` / `=` | 기호 |
| `V` | 백슬래시 | 기호 |
| `B` | ABC에서는 백틱, 한글 입력에서는 `₩` | 기호 |
| `N` | `?` | 기호 |

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
| `Space + V` | 백슬래시 | `|` |
| `Space + B` | ABC에서는 백틱, 한글 입력에서는 `₩` | 입력 소스에 따라 다름 |
| `Space + N` | `?` | — |

Shift 기호는 `Shift`를 먼저 누른 상태에서 `Space`를 약 50ms 홀드한 뒤 대상 키를 누르는 순서가 가장 안정적입니다.

### 미디어 및 기능 키

| 조합 | 동작 |
| --- | --- |
| `Space + A/S/D` | 볼륨 감소 / 볼륨 증가 / 음소거 |
| `Space + 1~0` | F1~F10 |
| `Space + -` | F11 |
| `Space + =` | F12 |

일반 타이핑으로 A/S/D를 입력하려면 `Space`와 다음 키를 50ms 이내에 겹쳐 누르고, 미디어 기능을 사용하려면 `Space`를 50ms 이상 홀드한 뒤 A/S/D를 누르세요.

`Ctrl + Space`는 SpaceFN 컨트롤러에서 제외되어 macOS 입력 소스 전환 단축키로 그대로 전달됩니다.

## 타이밍 조정

[`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json)의 다음 두 값은 항상 같은 값으로 유지해야 합니다.

```json
"basic.to_if_held_down_threshold_milliseconds": 50,
"basic.to_delayed_action_delay_milliseconds": 50
```

- 현재 50ms는 빠른 반응을 위한 실험값입니다.
- 일반 타이핑에서 SpaceFN이 실수로 켜지면 두 값을 함께 `75`, `100`, `120` 또는 `150`으로 올리세요.
- 50ms에서 오작동이 늘면 실제로 사용해본 75ms 설정으로 되돌리는 것을 권장합니다.
- 단독 Space 허용 시간은 `basic.to_if_alone_timeout_milliseconds: 500`입니다.

## 호환 범위와 적용 범위

이 레이아웃은 HHKB와 유사한 물리 배열을 가진 표준 60% 이하 키보드를 대상으로 합니다. Karabiner-Elements는 키보드의 실제 물리 배열을 자동으로 판별하지 않으므로, 이 컴퓨터용 규칙은 연결된 모든 키보드에 적용됩니다. 연결된 키보드들이 호환되는 컴팩트 배열을 사용할 때 활성화하세요.

## 적용 대상과 구현 방식

- 장치 조건 없음: 이 컴퓨터에 연결된 모든 키보드에 적용됩니다.
- SpaceFN 상태 변수: `hhkb_spacefn`
- 규칙 1개, manipulator 38개(레이어 제어 1개 + 기능·기호 매핑 37개)
- `Space`를 50ms 홀드하면 `hhkb_spacefn = 1`이 되고, 손을 떼면 `key_up_value`로 `0`이 됩니다.
- 50ms 이전에 다른 키가 들어오면 `to_delayed_action.to_if_canceled`가 일반 공백을 복원합니다.
- 추가 modifier를 보존하므로 Shift 기호와 탐색 modifier를 사용할 수 있습니다.
- 장치 조건 없이 동작하며, SpaceFN 상태 변수에 따라 활성화된 레이어 매핑만 실행됩니다.

`key_up_value` 동작을 사용하므로 Karabiner-Elements 14.12.6 이상이 필요합니다.

이 설정은 특정 키보드의 vendor ID나 product ID를 요구하지 않습니다.

## 설치

설정 파일을 Karabiner-Elements의 complex-modifications 폴더에 복사합니다.

```bash
cp hhkb_spacefn_final.json ~/.config/karabiner/assets/complex_modifications/
```

그 다음 Karabiner-Elements의 **Complex Modifications**에서 `60% Ergo` 규칙을 활성화하세요.

## 파일

- [`hhkb_spacefn_final.json`](./hhkb_spacefn_final.json): Karabiner-Elements complex modification 설정
- [`README.md`](./README.md): 영문 문서
