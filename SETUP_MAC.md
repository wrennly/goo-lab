# Goo Lab — M1 Mac セットアップ手順

> Phase 0: Unity Editor を起動して 2D テンプレートでプロジェクトを開くまで。

---

## ✅ 完了基準

- [ ] Unity Hub が起動する
- [ ] Unity 6 LTS (Apple Silicon) がインストール済み
- [ ] WebGL Build Support モジュールが入っている
- [ ] `goo-lab` プロジェクトが Unity で開ける
- [ ] Git で push 済み（DIGITS 側からも見える）

---

## 1. Unity Hub のインストール

### 公式ダウンロード（推奨）

```
https://unity.com/download
```

→ "Download Unity Hub" ボタン → **Mac (Apple Silicon)** を選択

ダウンロード後、`UnityHubSetup.dmg` を開いてアプリケーションへドラッグ。

### または Homebrew

```bash
brew install --cask unity-hub
```

---

## 2. Unity アカウント作成 / ログイン

- Unity Hub 起動
- "Sign in" → Unity ID 作成（または既存アカウントでログイン）
- ライセンス: **Personal**（個人 / 売上 $200K 未満は無料）を取得

---

## 3. Unity Editor のインストール

Unity Hub の "Installs" タブ → **Install Editor**

- バージョン: **Unity 6.x LTS（最新の LTS）**
- アーキテクチャ: **Apple Silicon** ⭐ Intel 版を選ばないこと
- モジュール（必須にチェック）:
  - ✅ **WebGL Build Support**（Phase 1 出力ターゲット）
  - ✅ **Mac Build Support (IL2CPP)**（ローカル動作確認）
  - ✅ **Documentation**（オフライン参照用）
  - ⏭️ Windows / Linux / iOS / Android は後で追加可

ダウンロード ~10GB、5〜15 分。

---

## 4. プロジェクト作成

### 4-1. リポジトリ取得

DIGITS 側で `goo-lab` を GitHub に上げる前提。Mac 側：

```bash
cd ~/Developer  # または好きな場所
git clone git@github.com:<your-account>/goo-lab.git
cd goo-lab
```

### 4-2. Unity プロジェクト初期化

Unity Hub の "Projects" タブ → **New Project**

- テンプレート: **Universal 2D** （URP 2D, 推奨）
- Project name: `unity-project`
- Location: `~/Developer/goo-lab/`（クローン先）

→ `~/Developer/goo-lab/unity-project/` が生成される。

### 4-3. .gitignore 設定

`unity-project/` 直下に Unity 公式 `.gitignore` を配置。

```bash
cd ~/Developer/goo-lab/unity-project
curl -O https://raw.githubusercontent.com/github/gitignore/main/Unity.gitignore
mv Unity.gitignore .gitignore
```

### 4-4. 初コミット

```bash
cd ~/Developer/goo-lab
git add .
git commit -m "Phase 0: Unity 6 LTS + Universal 2D template"
git push
```

---

## 5. 動作確認

### Unity Editor 上

- 空のシーンが開く
- Hierarchy に `Main Camera` が見える
- Project ペインに Assets フォルダ
- Scene ビューでパン・ズームできる

### WebGL ビルド試走

`File > Build Settings` → Platform を **WebGL** に切り替え → **Switch Platform**
→ **Build And Run** → 空のページがブラウザで開けば OK。

---

## 6. Phase 0 完了タスク

DESIGN.md の Phase 0 完了基準：

- [ ] Rigidbody2D + Collider2D で球を落として跳ねる
- [ ] Shader Graph でメタボール試作
- [ ] WebGL ビルドが出る

公式チュートリアル `2D Beginner: Adventure Game`（Unity Learn）を一周してから上記に進むのが最短。

---

## 🛠 トラブルシューティング

| 症状 | 対処 |
|---|---|
| Unity Hub が起動しない | macOS のセキュリティ設定で許可、再起動 |
| Editor インストール失敗 | ディスク空き 30GB 以上確保、再試行 |
| `Apple Silicon` 選択肢が出ない | Unity Hub 自体が Intel 版の可能性、再 DL |
| WebGL ビルドが遅い | 初回はシェーダー圧縮で長い、2 回目以降は速い |

---

## 🔗 参考

- Unity Learn: https://learn.unity.com/
- 2D Beginner: Adventure Game: https://learn.unity.com/project/2d-beginner-adventure-game
- URP 2D Documentation: https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@latest

---

**次のドキュメント**: `SETUP_DIGITS.md`（アート生成環境構築 — Comfy UI on GB10）
