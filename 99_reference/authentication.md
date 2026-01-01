# 【資料】ローカル環境での認証設定

Codespacesでは自動で認証が行われていますが、現場のPCや自分のPCでGitを使ってGitHubにPushするには、**認証設定**が必要です。

現在、GitHubはセキュリティ強化のため、**アカウントのパスワードを使った認証（Push）を廃止**しています。

以下のどちらかの方法で設定する必要があります。

1. **HTTPS + 個人アクセストークン (PAT)**: 設定が比較的簡単。
2. **SSH鍵認証**: 初期設定は手前だが、一度設定すれば楽。**（推奨）**

## 方法1: HTTPS + 個人アクセストークン (PAT)

いつものパスワードの代わりに、**「Git専用の長いパスワード（トークン）」** を発行して使います。

### 手順1: トークンの発行

1. GitHubの右上のアイコン -> **[Settings]** をクリック。
2. 左メニューの一番下 **[Developer settings]** をクリック。
3. **[Personal access tokens]** -> **[Tokens (classic)]** を選択。
4. **[Generate new token (classic)]** をクリック。
5. **Note**: 何用のトークンか入力（例: `MyPrivatePC`）。
6. **Expiration**: 有効期限を設定（無期限にはしないのが安全ですが、学習用なら長めに）。
7. **Select scopes**: **`repo`** にチェックを入れる（これで読み書き権限がつきます）。
8. **[Generate token]** をクリック。
9. **表示された `ghp_` から始まる文字列をコピーして、メモ帳などに保存する。**
   ※ **重要:** この画面を閉じると二度と表示されません！

### 手順2: 認証に使う

ターミナルで `git push` をした時、ユーザー名とパスワードを求められます。

パスワード入力中は画面に何も表示されませんが、入力されています。

```bash
Username for '[https://github.com](https://github.com)': <あなたのGitHubユーザー名>
Password for 'https://...': <さっきコピーしたトークンを貼り付け>
```

#### Windowsの場合

Git for Windows をインストールしている場合、「Git Credential Manager」というポップアップ画面が出ることがあります。

その場合は [Token] タブを選び、そこにトークンを貼り付けてください。

## 方法2: SSH鍵認証 (推奨)

「秘密鍵（自分しか持っていない鍵）」と「公開鍵（誰に見せてもいい鍵穴）」のペアを作り、GitHubに鍵穴を登録しておく方法です。

一度設定すれば、パスワード入力不要で安全に通信できます。

### 手順1: 鍵ペアの作成 (`ssh-keygen`)

Git Bash (Windows) または ターミナル (Mac) を開き、以下のコマンドを入力します。

```bash
# -t ed25519 は最新の暗号化方式を指定しています
# -C の後ろはコメントです（自分のメアドなど）
ssh-keygen -t ed25519 -C "your_email@example.com"
```

いくつか質問されますが、全て Enter キー連打（空欄のまま）でOKです。
これで `~/.ssh/` フォルダの中に鍵が作られました。

### 手順2: 公開鍵の中身をコピー

作成された「公開鍵（.pub）」の中身を表示してコピーします。

#### Windows (Git Bash)

```bash
cat ~/.ssh/id_ed25519.pub
# 表示された ssh-ed25519 AAAA... をコピー
```

#### Mac

```bash
pbcopy < ~/.ssh/id_ed25519.pub
# これでクリップボードにコピーされます
```

### 手順3: GitHubに登録

- GitHubの **[Settings]** -> **[SSH and GPG keys]** をクリック。
- **[New SSH key]** をクリック。
- **Title**: 自分のPC名など（例: `MacBookPro`）。
- **Key**: さっきコピーした内容を貼り付ける。
- **[Add SSH key]** をクリック。

### 手順4: 接続テスト

設定が成功したか確認します。

```bash
ssh -T git@github.com
```

- `Are you sure you want to continue connecting?` と聞かれたら `yes` と入力。
- `Hi <ユーザー名>! You've successfully authenticated...` と表示されれば成功です！

### 手順5: リモートURLの切り替え

もし `https://...` でリポジトリをクローンしていた場合、SSH用のURLに変更する必要があります。

```bash
# 現在のURL確認
git remote -v

# SSH用に変更（git@github.com:... という形式）
git remote set-url origin git@github.com:ユーザー名/リポジトリ名.git
```

これで、以降はパスワードなしで `git push` が可能になります。

## コラム ： 一時的に別のアカウントにする
