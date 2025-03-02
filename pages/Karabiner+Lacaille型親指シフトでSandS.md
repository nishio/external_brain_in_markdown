---
title: "Karabiner+Lacaille型親指シフトでSandS"
---

日本語の入力を親指シフトにしてからプログラム書くとSandS（スペース長押しでシフトキー）の機能が欲しくなる
- [[Macで親指シフト日記2020-01#5e02ec55aff09e0000449fba]]
    - というよりむしろ右手親指が変換キーの上でスタンバイしてるけどプログラムを書く時には全く必要ないのでこれが英字のシフトになれば良いのではないか…？
    - できた [[かなキーを英数モードではシフトキーにもする]]
    - この話は今回はしない

- [[karabiner-element]]のSandS
    - [https://pqrs.org/osx/karabiner/complex_modifications/#spacebar](https://pqrs.org/osx/karabiner/complex_modifications/#spacebar)
    - 英数モードだけとかできないのでスペースキーが親指シフトの左シフトとして使われてることとぶつかる
        - Lacailleが左親指シフトと小指シフトを区別するから
    - なら英数モード限定すればいい
        - ~/.config/karabiner/karabiner.jsonを直接編集して解決した

条件指定
json

```json
"conditions": [
  {
    "input_sources": [
      {
        "input_mode_id": "com.apple.inputmethod.Roman"
      }
    ],
    "type": "input_source_if"
  }
],
```


全体
json

```json
{
  "description": "Change spacebar to left_shift. (Post spacebar if pressed alone)",
  "manipulators": [
    {
      "conditions": [
        {
          "input_sources": [
            {
              "input_mode_id": "com.apple.inputmethod.Roman"
            }
          ],
          "type": "input_source_if"
        }
      ],
      "from": {
        "key_code": "spacebar",
        "modifiers": {
          "optional": [
            "any"
          ]
        }
      },
      "to": [
        {
          "key_code": "left_shift"
        }
      ],
      "to_if_alone": [
        {
          "key_code": "spacebar"
        }
      ],
      "type": "basic"
    }
```


