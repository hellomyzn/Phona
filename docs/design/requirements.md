# Phona
## 🎯 1. プロジェクト概要

英語学習者（中級）が、自分の発音を音素レベルで可視化し、改善ポイントを理解できる
**英語発音矯正サービス** を開発する。

まずはローカルで動く最小デモ（MVP）を作成し、
「発音 → 音声解析 → IPA可視化」の一連の流れが実現可能か検証する。

---

## 🔍 2. 想定ユーザー

* 英語中級者
* 日常会話レベルの発音を改善したい人
* 日本語母語話者など、特定音素が苦手な学習者

---

## 🎤 3. MVPで実現する機能（ローカル・最小実装）

### ✔️ 必須

1. **音声録音（FE）**

   * ブラウザ（React/TS）でマイク録音
   * 3秒以内の短い音声

2. **音声アップロード → BEへ送信**

   * `POST /analyze`
   * フォーマット：webm → BEでwavへ変換

3. **Whisperローカル推論（BE）**

   * whisper-small or base
   * 認識テキストを取得する

4. **テキスト → IPA変換**

   * CMU Dict → ARPABET
   * ARPABET → IPAテーブルで変換

5. **IPAの比較**

   * 正解IPAと一致率を算出
   * 音素単位で色分け

6. **結果表示（FE）**

   * 認識された単語
   * 正解IPA
   * 推定IPA
   * 一致率
   * 改善ポイントのリストアップ

### ❌ 対象外（後で実装）

* リアルタイム音声ストリーミング
* 音素分類モデル
* ユーザーアカウント
* DB保存
* アプリ化（iOS）

---

## ⚙️ 4. 技術スタック

### Frontend

* React / TypeScript
* Vite or Next.js（後で選定）
* Web Audio API
* Axios or Fetch

### Backend

* Python 3.11+
* FastAPI
* Uvicorn
* pydantic（型定義）
* whisper or whisper.cpp
* FFMPEG（音声変換）

---

## 🧱 5. アーキテクチャ（MVP版）

```
frontend/
  └── audio/
  └── api/
backend/
  ├── app/
  │    ├── controller/
  │    ├── service/
  │    ├── repository/
  │    ├── model/
  │    ├── schema/
  │    ├── utils/
  └── tests/
```

### Controller

* 受け取った音声の処理フロー開始
* `/analyze` API

### Service

* 音声変換
* whisper推論
* IPA変換
* 比較処理

### Repository

* 将来的にデータ保存が必要になった場合に導入
  （MVPではメモリ or ファイル扱い）

### Model / Schema

* IPAResult
* AnalysisRequest
* Domain Objects

---

## 🧪 6. テスト戦略（TDD）

### 優先度の高いテスト

1. IPA変換（辞書 → IPA）
2. IPA比較ロジック（差分）
3. Service 層のユニットテスト
4. Controller のFastAPI APIテスト（音声ファイルモック）

Whisper自体の精度はTDD対象外（外部依存のため）。

---

## 🚀 7. MVPの成功条件

* ローカルで音声録音し、
* Whisperで推論し、
* 正解IPAと差分が可視化できること

---

---

# 🧪 まず作るべき「ローカルデモ」のスコープ

最小の動線（一本線）：

**録音 → 音声送信 → Whisper → IPA変換 → 差分 → 表示**

ここにリアルタイムや複雑なモデルは入れない。

デモに使う単語は *banana*（固定）。
