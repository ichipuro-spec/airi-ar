# Airi ARポスター（テスト版）🎤✨

スマホのカメラで **Airiのポスター** を映すと、その上に新曲
**「Don't Stop Dreaming!」MV（0:45〜1:02 の17秒）** が浮かんで再生される Web AR です。

- ✅ スマホのブラウザだけで動く（**アプリ不要**）
- ✅ **GitHub Pages** で無料公開できる
- ✅ **A-Frame + AR.js**（画像認識／NFT方式）
- ✅ ポスター画像そのものをマーカーに使用
- ✅ iPhone（Safari）／Android（Chrome）対応

> ⚠️ これは「ポスターに向けるとMVが出る」を確認するための **テスト版** です。
> 動画の位置やサイズの厳密な合わせ込みは、実機で見ながら微調整してください（後述）。

---

## 📁 フォルダ構成

```
airi-ar/
├─ index.html            … ARアプリ本体
├─ assets/
│   ├─ poster.jpg        … ポスター画像（参考用）
│   ├─ poster.iset       … 画像認識データ（自動生成）
│   ├─ poster.fset       … 画像認識データ（自動生成）
│   ├─ poster.fset3      … 画像認識データ（自動生成）
│   └─ airi-mv.mp4       … MV（0:45〜1:02 の17秒・H.264/AAC・iOS対応）
└─ README.md
```

`poster.iset / .fset / .fset3` の3つが「ポスターを見分けるための地図データ」です。
**この3つは必ずセットで** GitHubに上げてください。

---

## 🚀 GitHub Pages での公開手順

### 1. リポジトリを作る
1. GitHub にログイン → 右上「＋」→ **New repository**
2. リポジトリ名を入力（例：`airi-ar`）
3. **Public** を選択して「Create repository」

### 2. ファイルをアップロード
**かんたんな方法（ドラッグ＆ドロップ）**
1. 作ったリポジトリの「**Add file**」→「**Upload files**」
2. `index.html` と `README.md` と **`assets` フォルダの中身ごと** ドラッグ
   - `assets` フォルダの構造を保ったまま上げてください
3. 下の「**Commit changes**」を押す

**コマンドが使える方法（Git）**
```bash
cd airi-ar
git init
git add .
git commit -m "Airi AR poster test"
git branch -M main
git remote add origin https://github.com/＜あなたのユーザー名＞/airi-ar.git
git push -u origin main
```

### 3. Pages を有効化
1. リポジトリの「**Settings**」→ 左メニュー「**Pages**」
2. **Source** を「**Deploy from a branch**」
3. **Branch** を「**main**」/ フォルダ「**/(root)**」→ **Save**
4. 1〜2分待つと、上部に公開URLが出ます：
   ```
   https://＜あなたのユーザー名＞.github.io/airi-ar/
   ```

> 📌 GitHub Pages は自動で **https** になります。
> AR（カメラ）は **https でないと動かない** ので、この公開URLが必須です。
> （`file://` でローカルに開いてもカメラは起動しません）

---

## 📱 QRコードの作り方

公開URL（例：`https://＜ユーザー名＞.github.io/airi-ar/`）を QRコードにします。

**おすすめサイト（無料・登録不要）**
- [https://qr.quel.jp/](https://qr.quel.jp/)
- [https://www.cman.jp/QRcode/](https://www.cman.jp/QRcode/)
- Google Chrome：アドレスバー右クリック →「このページのQRコードを作成」

**手順**
1. 上記サイトに公開URLを貼り付け
2. QRコードを生成 → 画像をダウンロード
3. ポスターやチラシに印刷／LINEやSNSで配布

> 💡 ポスター下部の「QR」枠（Instagram / YouTube / TikTok）の横などに、
> この **ARのQR** を1つ追加すると体験につながります。

---

## 🎬 遊び方（ユーザー向け説明文）

1. QRコードを読み込む
2. 「**スタート ▶**」を押す
3. カメラの使用を **許可**
4. **ポスター全体** を画面の枠に合わせる
5. ポスターの上にMVが出て再生されます🎶

- iPhone → **Safari** で開いてください
- Android → **Chrome** で開いてください
- 明るい場所で、ポスター全体がはっきり映ると認識しやすいです

---

## 🔧 動画の位置・サイズの微調整

ポスターと動画がズレる／大きすぎる・小さすぎる場合は、
`index.html` 内のこの部分の数字を変えてください。

```html
<a-video
  id="ar-video"
  src="#airi-mv"
  position="400 565 1"   ←  左右(X) 上下(Y) 手前(Z)
  rotation="0 0 0"
  width="800"            ←  横幅（MVは16:9なので height は width×0.56 が目安）
  height="450">          ←  高さ
</a-video>
```

- **動画が大きすぎる** → `width` と `height` を同じ比率で小さく（例：600 / 338）
- **位置がズレる** → `position` の数字を増減（単位はおよそポスターのピクセル）
- 基準：ポスター画像は **800 × 1132 px**。中心は `400 566` 付近です。

数字を変えたら保存して、もう一度 GitHub にアップ（上書きコミット）すれば反映されます。

---

## ❓ うまく動かないとき

| 症状 | 対処 |
|------|------|
| カメラが起動しない | URLが **https**（github.io）か確認。`file://` ではNG |
| 「許可」を押したのに映らない | ブラウザ設定でカメラがブロックされていないか確認 |
| ポスターを認識しない | 明るい場所で、ポスター全体・正面・手ブレなしで映す |
| 動画は出るが音が出ない | 一度画面をタップ（iOSは操作後に音が出ます） |
| iPhoneで動かない | **Safari** で開く（アプリ内ブラウザ/LINE等は不可な場合あり） |

> 📌 アプリ内ブラウザ（Instagram・LINE・TikTok内など）はカメラ制限があります。
> QRから開いたあと「**Safari/Chromeで開く**」を選ぶと安定します。

---

## 🛠 技術メモ

- 画像認識データ（`.iset/.fset/.fset3`）は、`poster.jpg` から
  [@webarkit/nft-marker-creator-app](https://github.com/WebARKit/NFT-Marker-Creator) で生成しています。
- **ポスターのデザインを変えたら、マーカーデータも作り直しが必要**です：
  ```bash
  npm install @webarkit/nft-marker-creator-app
  node node_modules/@webarkit/nft-marker-creator-app/src/NFTMarkerCreator.js \
    -i assets/poster.jpg -o assets/
  ```
- 動画は `ffmpeg` で 0:45〜1:02（17秒）を切り出し、iOS再生用に
  H.264 / yuv420p / AAC / `+faststart` で書き出しています。
- iPhoneでより安定した画像認識が必要になったら、同じA-Frameで使える
  **MindAR**（iOS相性◎）への移行も検討できます。
