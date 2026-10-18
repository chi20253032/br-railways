# アカウント機能の設定

アカウントは Firebase Authentication で認証し、ログイン後の「再開後に興味のある活動分野」を Cloud Firestore に保存します。パスワードをこのリポジトリやブラウザー内に保存しません。Firestore のルールは各ユーザーが自分のUIDのデータだけ扱えるように制限しています。

## Firebase 側の設定

1. Firebase Console でプロジェクトを作成し、Web アプリを追加します。
2. Authentication の「ログイン方法」で「メール/パスワード」と「Google」を有効にします。Googleを有効にする際は、プロジェクトの公開名とサポートメールも指定します。
3. Authentication の設定にある承認済みドメインへ、公開サイトのホスト名（brrailway.f5.si）を追加します。ローカル検証には localhost も追加します。
4. Firebase のプロジェクト設定 > 全般 > マイアプリから Web アプリの設定値を取得し、ルートの firebase-config.js のプレースホルダーを置き換えます。必要な値は apiKey、authDomain、projectId、appId です。
5. Cloud Firestore のデータベースを作成します。リージョンを選んで本番モードで開始してください。
6. Firebase CLI をインストールしてログインし、このリポジトリのルートからセキュリティルールをデプロイします。

`npm install -g firebase-tools`

`firebase login`

`firebase deploy --only firestore:rules`

7. HTTPS でサイトを開き、メール登録またはGoogleログインを試します。クルー募集欄で興味のある活動分野を選ぶと、アカウントに保存できます。

リポジトリの firebase.json と firestore.rules は、Firebase プロジェクト mofu-br へこのアクセスルールをデプロイする設定です。Firestoreを作成する前にルールをデプロイすることはできません。

Firebase の Web 設定値はブラウザーに公開される識別情報です。秘密鍵として扱う値ではありません。Firebase Console で Web API キーの利用先を公開サイトに制限し、Authentication のメール列挙保護も有効にしてください。Firestore はルールをデプロイするまで、アカウントの活動分野の保存は利用できません。

## 含まれる機能

- メールアドレスと8文字以上のパスワードで登録・ログイン
- Googleアカウントでログイン（スマートフォンはリダイレクト方式）
- 表示名の登録、確認メールの送信
- パスワード再設定メール
- ログアウトとログイン状態の表示
- アカウント単位での気になる活動分野の保存
- モバイル対応のアカウントダイアログ

アカウントは認証用です。クルーへの応募は引き続き公式Discordで受け付けます。Firebase のプロジェクト設定が入っていない間は、アカウント画面に設定案内が表示されます。
