# 🔥 Firebase 共有ランキング セットアップ手順

このゲームは Firebase Realtime Database を使って、
**全ユーザーのスコアをリアルタイムで共有**します。

---

## ① Firebase プロジェクト作成

1. [https://console.firebase.google.com](https://console.firebase.google.com) にアクセス
2. **「プロジェクトを作成」** をクリック
3. プロジェクト名を入力（例: `coin-suika`）→ 続行 → 作成

---

## ② Realtime Database を有効化

1. 左メニュー → **「Realtime Database」**
2. **「データベースを作成」** をクリック
3. リージョン: `asia-southeast1（シンガポール）` を選択
4. セキュリティルール: **「テストモードで開始」** を選択
   → （後で変更OK）

---

## ③ セキュリティルール設定（重要）

Realtime Database → 「ルール」タブ → 以下に変更して **「公開」**:

```json
{
  "rules": {
    "rankings": {
      ".read": true,
      ".write": true
    }
  }
}
```

---

## ④ ウェブアプリを登録してAPIキーを取得

1. プロジェクト設定（歯車アイコン）→ **「マイアプリ」**
2. **「</>（ウェブ）」** アイコンをクリック
3. アプリのニックネームを入力（例: `coin-suika-web`）
4. 「Firebase Hosting も設定する」は **チェックしない**
5. **「アプリを登録」** をクリック

以下のような設定が表示されます:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "coin-suika.firebaseapp.com",
  databaseURL: "https://coin-suika-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "coin-suika",
  storageBucket: "coin-suika.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

---

## ⑤ index.html に設定を貼り付ける

`index.html` を開いて、以下の箇所を探します:

```javascript
const FIREBASE_CONFIG = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  ...
};
```

この部分を **④で取得した設定に書き換えて** 保存します。

---

## ⑥ GitHub Pages にデプロイ

1. GitHub に新しいリポジトリを作成
2. `index.html` と `README.md` をアップロード
3. Settings → Pages → Source: **main / root** に設定
4. 数秒後に `https://ユーザー名.github.io/リポジトリ名/` で公開！

---

## ✅ 動作確認

- ゲームを開くと右上に **「🟢 LIVE」** と表示される → Firebase接続OK
- **「🔴 LOCAL」** の場合は設定が未完了（ローカルモードで動作）
- ランキングタブを開くと全ユーザーのスコアがリアルタイム表示される
- スコアを出してOKボタンを押すとFirebaseに保存され、他のユーザーにも見える

---

## ❓ よくある質問

**Q: 無料でどのくらい使えますか？**
A: Firebase 無料プラン（Spark）で月100万回の読み書きが無料です。
   個人ゲームであれば無料枠で十分です。

**Q: セキュリティは大丈夫ですか？**
A: テストモードではスコアの書き込みが誰でもできます。
   スパム対策が必要な場合はルールを強化してください。

**Q: ランキングはリアルタイム更新されますか？**
A: はい！他のユーザーがスコアを登録すると、
   ランキングタブを開いている全員の画面が自動更新されます。
