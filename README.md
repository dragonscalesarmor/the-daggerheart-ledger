# Daggerheart Ledger

A shared, self-hosted character & table tracker for Daggerheart groups — built for a Discord-sized group of players and DMs, not tied to any account or app store.

- **Players** create characters, track HP/Stress/Hope/Armor, level up (with rollback if you misclick), pick real domain cards for their class and level.
- **DMs** create and run their own table(s), see only their own tables plus anyone not yet sorted into one — never another DM's table, even if several DMs share the same link.
- **No login for anyone.** A short account code (auto-generated, no password) is all that ties characters and tables to a person, and it's portable across devices.
- Works on desktop, mobile, whatever browser your group already uses.

## ⚠️ Before you use this: deploy your own copy

**Don't just open this file and start playing — it won't be connected to anything until you set up your own free database.** This repo is a *template*, not a hosted service. Every group that wants to use this needs their own:

1. A free Firebase project (Google account, no credit card needed for what this uses)
2. This code hosted somewhere with a stable link (GitHub Pages, free, is what these instructions assume)

That's it — no server to run, no ongoing maintenance, and it's yours: your data never touches anyone else's, including the person who wrote this.

**👉 Full step-by-step setup: see [`deployment-guide.md`](./deployment-guide.md).** It's written for people with zero web-hosting experience — if you can copy and paste, you can do this. Roughly 15–20 minutes, once, ever.

## Getting your own copy of this code

Click **"Use this template"** near the top of this repo's GitHub page → gives you a fresh copy under your own account, with clean history, ready to follow the setup guide from step 1.

(If you don't see that button, you can also just download `index.html` directly and follow the guide from Part 6 onward — same result, one extra manual step.)

## What's actually in the box

- `index.html` — the entire app. Single file, no build step, no dependencies to install. Open it in any text editor if you're curious how it works.
- `deployment-guide.md` — the setup walkthrough (Firebase + GitHub Pages).

## A few honest limitations

- This isn't built with real user accounts. The account-code system and DM passcode-free role split are convenience features for a trusted group, not airtight security. Fine for a Discord-sized group; don't expect it to survive someone actively trying to mess with it.
- All game data (classes, ancestries, domain cards, etc.) is transcribed from the Daggerheart SRD as of when this was built. Daggerheart itself is © Darrington Press — this is an unofficial fan tool, not an official product.
- No official support — this was built collaboratively in a chat with Claude (Anthropic), and its author is a hobbyist, not a professional dev. It works well for its intended use, but treat it accordingly.

## Questions / found a bug?

This is fan-made and shared as-is. Feel free to fork it, tweak it, fix things, or build on top of it for your own group.
