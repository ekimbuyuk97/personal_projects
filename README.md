# AI Digest

A twice-daily AI news digest delivered to your inbox, running entirely on GitHub Actions — no server required.

Each email has two parts: a short digest of the day's top AI news, and a longer tiered deep-dive. It tracks what it's already covered so you never get duplicate stories, and maintains ongoing threads for developing stories.

Focused on Anthropic, Google DeepMind, and OpenAI — with a product manager lens.

---

## What you get

- **Top AI Industry News** — significant developments since the last run
- **Anthropic Spotlight** — new posts, research, and exec activity
- **AI for PMs** — named interviews, podcast episodes, and essays relevant to product work at AI labs
- **Deep Dive** — thorough coverage with multiple viewpoints, sourced claims, and further reading, tiered by relevance (P0–P3)

Runs at 8am and 8pm ET by default. Quiet cycles are honest — no padding.

---

## Setup

### 1. Fork this repo

Click **Fork** in the top right on GitHub.

### 2. Get your API keys

**Anthropic API key** — [console.anthropic.com](https://console.anthropic.com) → API Keys → create new

**Resend API key** — [resend.com](https://resend.com) → sign up for free → API Keys → create new

On Resend's free tier, you can only send to email addresses you've verified. Go to **Resend → Emails → Verified addresses** and add yours.

### 3. Add secrets to your fork

In your forked repo: **Settings → Secrets and variables → Actions → New repository secret**

Add these three:

| Secret | Value |
|--------|-------|
| `ANTHROPIC_API_KEY` | Your Anthropic API key |
| `RESEND_API_KEY` | Your Resend API key |
| `RECIPIENT_EMAIL` | The email address to deliver to |

### 4. Enable Actions

GitHub sometimes disables Actions on forks. Go to the **Actions** tab in your fork and click **"I understand my workflows, go ahead and enable them"** if prompted.

### 5. Test it

Actions → **AI Digest** → **Run workflow** → **Run workflow**

Check your inbox. If the email doesn't arrive, check the Actions log for errors — the most common issue is an unverified recipient address on Resend's free tier.

---

## Customizing

**Schedule** — edit the cron expressions in `.github/workflows/ai-digest.yml`. Times are in UTC. Use [crontab.guru](https://crontab.guru) to calculate.

**Prompt** — edit `ai-digest/prompt.md` to change sources, focus areas, tone, or structure.

**State** — `ai-digest/state.json` is auto-updated after each run to track seen stories. Don't edit it manually unless you want to reset history.

---

## How it works

1. GitHub Actions runs on a cron schedule
2. Claude Code CLI reads the prompt and state, searches the web, synthesizes the digest
3. The email is sent via the Resend API
4. Updated state is committed back to the repo

Everything runs in GitHub's cloud — your machine doesn't need to be on.
