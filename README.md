# UIAPduino HID Board Manager Files

Arduino IDE のボードマネージャー用インデックスファイルです。  
UIAPduino (HID ProMicro CH32V003) シリーズを Arduino IDE で使えるようにします。

---

## インストール方法

### 1. ボードマネージャーの URL を追加

Arduino IDE を開き、メニューから  
`ファイル` → `環境設定`（macOS: `Arduino IDE` → `設定`）を開きます。

「追加のボードマネージャのURL」欄に以下を入力して **OK** を押します:

```
https://github.com/tarosay/board_manager_files/raw/main/package_uiap_hid_index.json
```

### 2. ボードをインストール

`ツール` → `ボード` → `ボードマネージャ` を開きます。  
検索欄に `UIAPduino` と入力し、**UIAPduino HID** をインストールします。

### 3. ボードを選択

`ツール` → `ボード` → `UIAP_HID` → **HID ProMicro CH32V003** を選択します。

---

## 対応ボード

### HID ProMicro CH32V003

1 種類のボードに統合されています。  
`ツール` メニューで USB モード・UART・最適化レベルを選択します。

#### USB メニュー

| 設定 | 機能 |
|------|------|
| WebHID Only（デフォルト） | WebHID 双方向通信（Chrome / Edge 対応） |
| Keyboard+Mouse | USB キーボード ＋ マウス |
| Keyboard+Mouse+WebHID | USB キーボード ＋ マウス ＋ WebHID 双方向通信 |
| Terminal HID | HID シリアルターミナル |

#### U(S)ART support メニュー

| 設定 | 機能 |
|------|------|
| None — use UIAPSerial（デフォルト） | 軽量 UART ラッパー。Flash 消費を最小に抑える |
| HardwareSerial (Serial / USART1) | Arduino 標準の `Serial` を使用（+約 4.7 KB） |

#### Optimize メニュー

| 設定 | フラグ |
|------|--------|
| Smallest (-Os) with LTO（デフォルト） | `-Os -flto` |
| Fast (-O1) with LTO | `-O1 -flto` |
| Faster (-O2) with LTO | `-O2 -flto` |
| Fastest (-O3) with LTO | `-O3 -flto` |

---

## バージョン履歴

### 1.1.0（最新）

- **ボードを 1 種類に統合**
  - `HID ProMicro CH32V003`・`HID ProMicro CH32V003 KBD+Mouse` など 3 ボードを  
    `HID ProMicro CH32V003` 1 ボードに統合
  - FQBN: `UIAP_HID:ch32v:CH32V003:opt=oslto`
- **USB メニューを追加**
  - WebHID Only（デフォルト）/ Keyboard+Mouse / Keyboard+Mouse+WebHID / Terminal HID
  - デフォルトを Terminal HID → **WebHID Only** に変更
- **U(S)ART support メニューを追加**
  - None/UIAPSerial（デフォルト）/ HardwareSerial を切り替え可能に
- **Optimize メニューを整理**
  - LTO なしオプションと `-Og` / `-O0` を削除
  - すべての最適化レベルで LTO (`-flto`) を有効化

### 1.0.4

- **Tone ライブラリ**を追加
  - `tone(pin, freq)` がハードウェア PWM による真のノンブロッキング無限再生に対応
  - `tone(pin, freq, duration)` で指定時間だけ鳴らして自動停止
  - タイマーチャネルがないピンはソフトウェアビットバンフォールバック
  - スケッチ例: ToneBasic / ToneDuration / ToneNoTone

### 1.0.3

- **Mouse.moveLarge()** を追加
  - `-127〜127` の制限を超える大きなマウス移動を複数ステップに分割して送信
  - `Mouse.moveLarge(x, y, wheel, steps)` — wheel・steps は省略可能

### 1.0.2

- **Keyboard.write()** の信頼性を改善
  - 特殊キー（矢印・BackSpace・Enter など）の取りこぼしを修正
  - press/release 間の待機時間を調整し USB ポーリングに確実に乗せるよう改善
- スケッチ例を追加: KeyboardPractice / KeyboardSwitch

### 1.0.1

- **WebHID** の送受信を 16 バイト対応に拡張
- EP3 の余分なポーリング送信を抑制（NAK で無送信）

### 1.0.0

- **HID ProMicro CH32V003 KBD+Mouse** ボードを追加
- `Keyboard` / `Mouse` ライブラリを追加
- **WebHID ライブラリ**を追加（EP3 双方向通信、Chrome / Edge 対応）
- Board Version Select メニューで V1.4 / V1.4 + WebHID を切り替え可能に

### 0.1.1

- HID ProMicro CH32V003 の安定版

### 0.1.0

- 初回リリース

---

## 関連リンク

| リンク | 内容 |
|-------|------|
| [arduino_core_ch32](https://github.com/tarosay/arduino_core_ch32) | Arduino コア本体・ライブラリ・サンプル |
| [GitHub Issues](https://github.com/tarosay/arduino_core_ch32/issues/new) | バグ報告・要望 |

---

## 対応 OS

| OS | 状況 |
|----|------|
| Windows | 動作確認済み（Arduino IDE 2.0 以上） |
| Linux | 動作確認中 |
| macOS | 動作確認中 |
