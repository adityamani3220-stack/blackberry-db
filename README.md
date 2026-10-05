# 🫐 Blackberry Telegram Bot — Render Ready

This version is made for **Render Background Worker + Telegram long polling**. No Vercel webhook is needed.

## Features kept / added
- `/approve` or `/free` — reply to a user's message to make them FREE from anti-spam.
- `/unapprove` — reply to restore protection.
- `/spammer` or `/spam` — reply to a user's message to mark them as SPAMMER; the replied message is deleted and future messages are deleted automatically. The bot also tries to ban them.
- `/block` — alias of `/spammer`.
- `/unblock` — reply to user to unblock/unban.
- `/mute` and `/unmute` — reply-based admin controls.
- `/del` — reply to any message and delete it.
- Automatic spam protection: **3 messages in 3 seconds** (configurable) deletes the recent burst.
- After auto spam detection, admins get **FREE / SPAMMER / UNAPPROVE** buttons.
- Stylish `/start` and `/help` screens.
- Bot command menu is automatically registered with Telegram.
- User ID / chat ID with `/id`.
- `/ping` status.
- SQLite works without a separate database. Optional PostgreSQL is supported through `DATABASE_URL`.
- PostgreSQL table names use `bb_` prefix to avoid the old `approved_users` type collision.

## Telegram permissions
Make the bot a **group administrator** and enable at least:
- Delete messages
- Ban users (for `/spammer`/`/block`)
- Restrict members (for `/mute`/`/unmute`)

If the bot does not receive normal group messages, disable BotFather privacy mode with `/setprivacy`, or keep the bot as a group administrator.

## Render deployment
1. Upload this folder to GitHub.
2. In Render choose **New → Background Worker** and connect the GitHub repository.
3. Render can also read `render.yaml` as the Blueprint configuration.
4. Build command: `pip install -r requirements.txt`
5. Start command: `python bot.py`
6. Add Environment Variable:
   - `BOT_TOKEN` = your BotFather token
   - `SPAM_LIMIT` = `3`
   - `SPAM_WINDOW` = `3`
   - `BOT_TIMEZONE` = `Asia/Kolkata`
   - `DATABASE_URL` = optional. Leave empty if you want SQLite.

### Important about SQLite on Render
Render worker filesystems can be ephemeral. If the worker is restarted/redeployed, a local SQLite database may reset. For permanent approvals/block lists, create a Render PostgreSQL database and set its `DATABASE_URL` environment variable.

## Local test
```bash
pip install -r requirements.txt
python bot.py
```
