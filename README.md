# starter-git-with-github

開発現場で必須となる **Git（ソースコード管理）** の概念と操作を、実際に手を動かしながら学ぶためのハンズオン資料です。

SESエンジニアとして、どんな現場（新しいWeb系企業でも、歴史ある業務システム開発でも）に行っても通用する「基礎体力」をつけることを目的としています。

> **⚠️ 学習上の重要ルール**
> [Git公式ドキュメント](https://git-scm.com/book/ja) の情報が「最新かつ正確」な一次情報です。
> ここで記載した内容や、もし AI から回答を得た場合であっても、**必ず [Git公式ドキュメント](https://git-scm.com/book/ja) の記載を確認しながら実装する癖** をつけてください。

---

## 💻 開発環境 (Development Environment)

この勉強会では **GitHub Codespaces** を使用します。

面倒な環境構築は不要です。ブラウザさえあれば、すぐに学習を始められます。

1. **GitHubにログイン** してください（アカウントがない場合は作成してください）。

1. このリポジトリをフォークするため、右上の`fork`をクリックする（Forkの意味については [00. 歴史と概念](./00_history_and_concept/README.md#6-コラムforkフォークとは) で解説しています）

    ![start-fork](./assets/start-fork.png)

1. `Create fork`ボタンをクリックして、フォーク（自分のアカウントにコピーして新しいリポジトリを作成）します。

    ![select-fork-option](./assets/select-fork-option.png)

1. `Codespace`を起動するため、`Code`タブに移動し、右上にある緑色の`code`のプルダウンメニューを開き、`Codespace`タブを開き、`Create codespace on main`をクリックします。

    ![success-setting](./assets/start-code-space.png)

1. `Codespace`の生成にはしばらく時間がかかるため、しばらく待ちます。

    ![create-now](./assets/create-now.png)

1. `VSCode`が起動しますが、画面左下が`リモートを開いています...`の間は待ちます。

    ![vscode-setup-now](./assets/vscode-setup-now.png)

1. 画面左下が`Codespace`になった場合は、`Codespace`が起動完了しました

    ![vscode-setup-finish](./assets/vscode-setup-finish.png)

環境が立ち上がったら、左側のファイル一覧から学習したい章のフォルダを開いてください。

## Codespaces利用上の注意

- `Github`の`Codespaces`を利用します。`Codespaces`は設定によってはコストがかかるものなので [Codespace の利用上の注意](./CODE_SPACES_SERICE.md) はよく確認してください。
- コストをかけないためにも、セキュリティの意味でも、使い終わったら [停止方法](./CODE_SPACES_SERICE.md#3-停止方法) に従って停止することを推奨します。

---

## 📚 カリキュラム

環境が立ち上がったら、左側のファイル一覧から学習したい章のフォルダを開き、`README.md` を読み進めてください。

| 章 | タイトル | 学ぶこと |
| :--- | :--- | :--- |
| **00** | [歴史と概念](./00_history_and_concept/README.md) | なぜGitを使うのか？ / 集中型(SVN)と分散型(Git)の違い |
| **01** | [一人で進める開発の基本](./01_local_basic/README.md) | `init`, `add`, `commit` / 歴史の記録 |
| **02** | [平行世界を作る](./02_branch_and_merge/README.md) | `branch`, `merge` / 実験と統合 |
| **03** | [チーム開発のルール](./03_workflows/README.md) | `push`, `pull` / GitHub Flow と Git Flow |
| **04** | [失敗と修正](./04_fix_and_recovery/README.md) | `revert`, `reset` / コンフリクトの解消 |
| **05** | [現場で役立つ便利機能](./05_useful_tips/README.md) | `.gitignore`, `stash` / 調査テクニック / リバースマージ |
| **99** | [ローカルPCでの認証設定手順 (Windows/Mac)](./99_reference/authentication.md) | 資料：自分のPCからGitHubにPushするための設定方法（トークン / SSH） |

## この教材の進め方

本教材では、特定の便利な拡張機能（GUIツール）には頼りません。

**「コマンド操作 (CLI)」** を中心に学習します。

なぜなら、現場によっては便利なツールが禁止されていたり、黒い画面（ターミナル）しか使えないサーバー上で作業を求められることがあるからです。

どこでも通用するスキルを身につけましょう。

### 学習の基本サイクル

1. **説明を読む:** 各章の `README.md` を読みます。
2. **コマンドを打つ:** ターミナルで実際にコマンドを実行します。
3. **確認する:** 以下のコマンドで、歴史が正しく作られているか確認します。

    ```bash
    git log --oneline --graph --all
    ```

資料の中に Mermaid（フロー図） で正解の形が描かれています。 ターミナルに表示されたグラフが、資料の図と同じ形になっていれば成功です。

### 📝 重視する思想

このリポジトリでは、「実際に手を動かしてみる」ことを何より重視しています。

エンジニアの技術は、資料を読むだけで覚えたり、理解したりすることは難しいものです。

例えば、自動車教習所の教本を完璧に暗記したとしても、それだけで実際に車を運転できるようにはなりませんよね？

ハンドルを握り、アクセルを踏むという「実体験」がなければ、運転技術は身につきません。

ソフトウェア技術も同じです。

技術的な仕組みを知ることも大切ですが、実際に実行した経験こそが現場で役立ちます。

読むだけで終わらせず、ぜひご自身の手で実行してみてください。
