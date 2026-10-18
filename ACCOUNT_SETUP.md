# アカウント機能の設定

アカウントは Firebase Authentication のメール/パスワード認証を使います。サイトは静的ホスティングのままで、パスワードをこのリポジトリやブラウザー内に保存しません。ユーザー情報と認証セッションは Firebase が管理します。

## Firebase 側の設定

1. Firebase Console でプロジェクトを作成し、Web アプリを追加します。
2. Authentication の「Sign-in method」で「メール/パスワード」を有効にします。
3. Authentication の設定にある承認済みドメインへ、公開サイトのホスト名（brrailway.f5.si）を追加します。ローカル検証には localhost も追加します。
4. Firebase のプロジェクト設定 > 全般 > マイアプリから Web アプリの設定値を取得し、ルートの firebase-config.js のプレースホルダーを置き換えます。必要な値は apiKey、authDomain、projectId、appId です。
5. HTTPS でサイトを開き、「マイページ」から新規登録し、届いたメールでアドレスを確認します。

Firebase の Web 設定値はブラウザーに公開される識別情報です。秘密鍵として扱う値ではありません。Firebase Console で Web API キーの利用先を公開サイトに制限し、Authentication のメール列挙保護も有効にしてください。Firestore などを後から追加する場合は、公開状態のままにせず Security Rules を設定してください。

## 含まれる機能

- メールアドレスと8文字以上のパスワードで登録・ログイン
- 表示名の登録、確認メールの送信
- パスワード再設定メール
- ログアウトとログイン状態の表示
- モバイル対応のアカウントダイアログ

アカウントは認証用です。クルーへの応募は引き続き公式Discordで受け付けます。Firebase のプロジェクト設定が入っていない間は、アカウント画面に設定案内が表示されます。
