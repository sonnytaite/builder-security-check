# builder-security-check

**Five checks before anyone else uses the app you built with AI.**

An agent skill for people who built an app with Claude Code, Cursor, Codex, Lovable, Bolt or a similar tool and cannot read the code themselves. It checks the five mistakes that account for most published breaches of apps built this way, asks the questions the code cannot answer, and reports in plain language with a fix you can paste straight back to your coding tool.

```
 your app's code
       │
       ▼
 ┌──────────────────────────────────────────┐
 │ 1 secrets in the code or the browser     │
 │ 2 row-level security off                 │
 │ 3 routes that never check who is asking  │
 │ 4 no rate limiting on the doors          │
 │ 5 the browser calling paid services      │
 └──────────────────────────────────────────┘
       │  + the questions only you can answer
       │  + spending caps on every paid API
       ▼
 Ready for other people to use: NOT YET
 (2 to fix, 1 can't tell, 2 pass)  with a paste-ready fix for each
```

## Install

```sh
npx skills add sonnytaite/builder-security-check -g
```

Then, inside your project, in your coding agent:

```
/builder-security-check
```

Or just ask: "check whether this app is safe for other people to use."

## What it does

- Works out what your app is built with (hosting, database, logins, paid services) and tells you in a sentence.
- Checks the five failures against the code and marks each **PASS**, **FIX** or **CAN'T TELL**. A check it could not finish is counted and named, never dropped and never called a pass.
- Asks the questions the code cannot answer: two-factor sign-in on the accounts that own the platform, GitHub's free scanners, tested backups, least privilege, spending caps on every paid API.
- Names the red lines where this check is not enough and you should get professional help: taking payments yourself, health, financial or children's data, personal data at scale, an app that has already been breached.
- Reads only. It changes nothing until you say yes to a specific fix, and it never prints the value of a key it finds.

## Why these five

Published scans of apps built with AI tools keep finding the same handful of mistakes. CVE-2025-48757 (Matt Palmer, 2025): of 1,645 Lovable-built apps scanned, 170 returned their users' rows to anyone holding the app's public key, because row-level security was missing or incomplete. The scanning services that followed report that the majority of unreviewed apps of this kind have at least one of the same issues, typically missing row-level security or an exposed key. AI coding tools optimise for an app that works, not an app that is safe; these five are the difference.

Sources: [CVE-2025-48757, Matt Palmer's disclosure](https://mattpalmer.io/posts/2025/05/CVE-2025-48757/) · [CVE-2025-48757 at SentinelOne](https://www.sentinelone.com/vulnerability-database/cve-2025-48757/) · [Lovable security risks, Vibe App Scanner](https://vibeappscanner.com/risks/lovable) · [the vibe coder's pre-launch checklist](https://dev.to/hacksafe/the-vibe-coders-pre-launch-security-checklist-25-checks-for-cursor-lovable-bolt-replit-apps-12i)

## What it does not do

- It reads the code it is given. It does not test the running app, probe your hosting, or log in to your dashboards.
- It does not replace a professional review where a red line applies.
- It does not know your platform's dashboard settings (rate limits, spending caps, two-factor). It asks you instead.

## Where it comes from

This is the security section of a longer brief I keep for non-technical builders in my family and community, turned into something an agent can run. The brief covers tool choice, hosting, databases and logins as well; the security checklist was the part people most needed and least used, so it became the skill.

MIT licence. Sonny Taite, 2026.
