# Personal Contact Website — GitHub Pages + Telegram

## Features
A clean three-field contact composer: To (fixed), Subject, and Message. Messages go to your Telegram channel through a Cloudflare Worker.

## Deploy frontend
1. Create a public GitHub repository (e.g. `contact`).
2. Upload `index.html` to the repository root.
3. GitHub repository → Settings → Pages → Deploy from a branch → main / root.
4. Your website appears at `https://USERNAME.github.io/contact/`.

## Telegram setup
1. Create a bot using @BotFather and keep the token secret.
2. Add the bot to your channel as an administrator allowed to post.
3. Find the channel chat ID (for public channels, `@channelusername` may work; private channels typically require a numeric ID).

## Deploy relay
1. Create a Cloudflare account and a Worker. Paste `worker.js` into the Worker editor and deploy.
2. Configure secrets `TELEGRAM_BOT_TOKEN` and `TELEGRAM_CHAT_ID` in Worker settings. Never add these to GitHub.
3. Set Worker variable `ALLOWED_ORIGIN` to `https://USERNAME.github.io` (origin only, without `/contact/`).
4. Edit `index.html`: replace `REPLACE_WITH_WORKER_URL` with your deployed Worker HTTPS URL.
5. Commit and test the live page.

## Security / limitations
This is a starter project, not abuse-resistant production infrastructure. Public forms can be spammed. Before sharing widely, add Cloudflare Turnstile validation server-side, rate limiting, and optionally a honeypot. The Worker currently accepts requests from the allowed browser origin, but CORS is not authentication and other HTTP clients can spoof Origin. For reliable abuse prevention, enforce server-side anti-bot checks. Avoid sending confidential personal data through Telegram. Cloudflare and GitHub free tiers have limits and terms that can change.
