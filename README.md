# Discord Bot

discord.py 製のBot。リマインド機能とリアクションによるグループ招待機能を搭載。

## セットアップ

1. [Discord Developer Portal](https://discord.com/developers/applications) でアプリケーションを作成し、Botを追加してトークンを取得
   - Bot > Privileged Gateway Intents で `SERVER MEMBERS INTENT` と `MESSAGE CONTENT INTENT` を有効化
2. 依存パッケージをインストール

```
pip install -r requirements.txt
```

3. `.env.example` を `.env` にコピーし、`DISCORD_TOKEN` に取得したトークンを設定

```
cp .env.example .env
```

4. OAuth2 > URL Generator で `bot` と `applications.commands` スコープ、`Manage Channels`(または `Manage Roles`) 権限を選んで招待URLを発行し、サーバーに招待

5. Bot起動

```
python bot.py
```

## 機能

### リマインド ([cogs/reminders.py](cogs/reminders.py))

- `/remind when:<日時> content:<内容>` — リマインド登録（絶対指定 `2026/07/01 12:00`、相対指定 `1週間後` `3日後` `2時間後` など）
- `/reminders` — 自分のリマインド一覧
- `/remind_cancel reminder_id:<ID>` — キャンセル

### グループ招待 ([cogs/group_invite.py](cogs/group_invite.py))

- `/group_create name:<グループ名> target_channel:<対象チャンネル> emoji:<絵文字> description:<説明>` — 案内メッセージを投稿しグループを作成（要 `manage_roles` 権限）
- `/group_list` — 設定済みグループ一覧
- `/group_delete message_id:<ID>` — グループ削除
- リアクション追加で対象チャンネルの閲覧・送信権限を自動付与、リアクション削除で取り消し

## 構成

```
discord-bot/
  bot.py              # エントリーポイント
  cogs/
    reminders.py      # リマインド機能
    group_invite.py   # グループ招待機能
  data/                # リマインド・グループ設定の永続化(自動生成)
  requirements.txt
  .env.example
```
