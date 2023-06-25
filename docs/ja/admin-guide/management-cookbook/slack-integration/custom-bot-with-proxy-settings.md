# Custom bot with proxy 設定

【概念図】
<img :src="$withBase('/assets/images/slack-bot-outline-custom-with-proxy.png')" alt="diagram-for-custom-bot-with-proxy">

Custom bot with proxy を Slack のワークスペースに導入するには、Slack アプリを作成・編集する必要があります。手順は以下の通りです。

## Custom bot with proxy を作成する

1. Slack API の[アプリページ](https://api.slack.com/apps)に移動し **Create an App** をクリックします。
   <img :src="$withBase('/assets/images/slack-custom-bot1.png')" alt="slack-custom-bot1">

2. **From an app manifest** をクリックします。
  <img :src="$withBase('/assets/images/slack-custom-bot2.png')" alt="slack-custom-bot2">

3. アプリをインストールするワークスペースを選択して **Next** をクリックします。
  <img :src="$withBase('/assets/images/slack-custom-bot3.png')" alt="slack-custom-bot3">

4. **YAML** タブに以下の App Manifest を貼り付けて **Next** をクリックします。
  <img :src="$withBase('/assets/images/slack-custom-bot4.png')" alt="slack-custom-bot4">

  ```yaml
  _metadata:
    major_version: 1
    minor_version: 1
  display_information:
    name: GROWI BOT
  features:
    bot_user:
      display_name: GROWI BOT
      always_online: false
    slash_commands:
      - command: /growi
        url: https://{Slackbot Proxy のドメイン名}/slack/commands
        description: Test Bot
        should_escape: false
    unfurl_domains:
      - {Slackbot Proxy の URL}
  oauth_config:
    redirect_urls:
      - https://{Slackbot Proxy のドメイン名}/slack/oauth_redirect
    scopes:
      bot:
        - channels:history
        - channels:join
        - chat:write
        - chat:write.public
        - commands
        - groups:history
        - im:history
        - links:read
        - links:write
        - mpim:history
        - team:read
  settings:
    event_subscriptions:
      request_url: https://{Slackbot Proxy のドメイン名}/slack/events
      bot_events:
        - link_shared
    interactivity:
      is_enabled: true
      request_url: https://{Slackbot Proxy のドメイン名}/slack/interactions
    org_deploy_enabled: false
    socket_mode_enabled: false
    token_rotation_enabled: false
  ```

5. アプリの概要を確認したら **Create** をクリックしてアプリを作成します。
  <img :src="$withBase('/assets/images/slack-custom-bot5.png')" alt="slack-custom-bot5">

## Slackbot Proxy を立ち上げる

1. `packages/slackbot-proxy` の配下に 新規ファイル`.env.development.local`を作成します。
1. 作成したファイルに任意の環境変数`SERVER_URI`を入力してください。

例: `SERVER_URI=http://localhost:8080`

3. さらに、[アプリページ](https://api.slack.com/apps)から作成した Bot を選択し、`Basic Information` > `App Credentials` の項目を確認します。

<img :src="$withBase('/assets/images/custom-bot-with-proxy-app-credentials.png')" alt="custom-bot-with-proxy-app-credentials">

その中から `Client ID`、`Client Secret`、`Signing Secret` を以下のように `.env.development.local` に追加します。

```
SERVER_URI={ Proxy の URI }
SLACK_CLIENT_ID={ Client ID }
SLACK_CLIENT_SECRET={ Client Secret }
SLACK_SIGNING_SECRET={ Signing Secret }
```

4. GROWI 本体サーバーとプロキシ用サーバー(`slackbot-proxy`)の両方を立ち上げてください。  
   プロキシ用サーバーは`yarn`, `yarn dev`で起動できます。

5. 管理画面の Slack 連携 にて **Custom bot with proxy** を選択してください。
   <img :src="$withBase('/assets/images/slack-bot-selecting-custom-bot-with-proxy.png')" alt="slack-bot-selecting-custom-bot-with-proxy">

## Custom bot with proxy を Slack のワークスペースへインストールする

1. 作成した Slack App の **Settings** から **Manage distribution** をクリックします。
1. **Share Your App with Other Workspaces** の 4 つの項目全てにチェックマークがついたら、**Activate Public Distribution** を押します。
   <img :src="$withBase('/assets/images/activate-public-dist.png')" alt="activate-public-dist">
1. ページ上部の **Add to Slack** ボタンを押します。
1. 遷移先の画面にて、Allow をクリックします。
   <img :src="$withBase('/assets/images/slack-bot-install-your-app-transition-destination.png')" alt="slack-bot-install-your-app-transition-destination">
1. **Congratulations!** と表示されたら Install が完了です。
1. GROWI bot を使いたいチャンネルに @example を使用して招待します。
   <img :src="$withBase('/assets/images/slack-bot-install-to-workspace-joined-bot.png')" alt="slack-bot-install-to-workspace-joined-bot">
   <img :src="$withBase('/assets/images/slack-bot-install-your-app-introduction-to-channel.png')" alt="slack-bot-install-your-app-introduction-to-channel">

::: warning

- `Illegal state, try it again.` と表示される場合は、**Go to install page** を押し、 **Add to Slack** から再度インストールしてください。
- `GROWI Bot installation failed..` と表示される場合は、**Add to Slack** ボタンから再度インストールしてください。
:::

## GROWI Custom Bot with proxy サービスへの登録

1. GROWI Custom Bot with proxy サービスへの登録を開きます。  
   **Access Token の発行** に各種トークンにアクセストークンが 2 種生成されていることを確認できます。
   アクセストークンは必要に応じて再発行できます。
1. Slack 上で `/growi register` と打ちます。
   <img :src="$withBase('/assets/images/slack-bot-growi-register.png')" alt="slack-bot-growi-register">
   <img :src="$withBase('/assets/images/slack-bot-register-modal.png')" alt="slack-bot-add-workspace">
1. 表示されるモーダルの GROWI URL に、対象 GROWI の URL を保存します。
1. 上記で発行されている Access Token Proxy to GROWI と Access Token GROWI to Proxy を入れ **Submit** ボタンを押します。

<img :src="$withBase('/assets/images/slack-bot-update-proxy-url.png')" alt="slack-bot-update-proxy-url">

成功した場合、 proxy サーバーの URL が表示されます。

<img :src="$withBase('/assets/images/slack-bot-input-proxy-url.png')" alt="slack-bot-input-proxy-url">

上記で取得した proxy サーバーの URL を **Custom Bot With Proxy Integration** の Proxy URL に入力し更新します。

## Custom bot with proxy の接続テストを実行する

1. 「Test connection」をクリックし、GROWI-Bot を招待した Slack チャンネルを入力します。
   <img :src="$withBase('/assets/images/slack-bot-test-introduction-custom-with-proxy.png')" alt="slack-bot-test-introduction">

2. 「Test」 ボタンをクリックします。

- 成功の場合  
   **Successfully sent to Slack workspace.** が Logs に表示され、
  赤丸で囲った部分に緑色のチェックマークが表示されます。GROWI-Bot を招待した Slack チャンネルで確認してみましょう。

  - GROWI 側
    <img :src="$withBase('/assets/images/slack-bot-test-success-custom-with-proxy.png')" alt="slack-bot-test-success">
  - Slack 側
    <img :src="$withBase('/assets/images/slack-bot-test-success-at-slack-app.png')" alt="slack-bot-test-success-at-slack-app">

- 失敗の場合  
  [接続テスト時のエラーログ](/ja/admin-guide/management-cookbook/slack-integration/#接続テスト時のエラーログ)を参照してください。

全ての設定が完了したら [GROWI bot でできること](/ja/admin-guide/management-cookbook/slack-integration/#growi-bot-でできること)を参照してください。
