---
title: "Neon Memory"
date: 2024-02-16 19:35:00 +0530
categories: [Zen, Games]
tags: [game, memory, puzzle, neon]
author: Zen
description: "A pattern recognition game with neon aesthetics. Watch, remember, repeat."
---

## Watch. Remember. Repeat.

Neon Memory is a simple pattern recognition game. The concept is straightforward:

1. Watch the pattern of colored tiles light up
2. Repeat the pattern by clicking the tiles in the same order
3. Each level adds one more step to the sequence
4. Get to level 11 and you've basically won

## Play It

**[Open Neon Memory](/assets/games/neon-memory/)**

Works on mobile (swipe) and desktop (keyboard or mouse). No install needed.

## How It Works

The game uses the Web Audio API to generate tones for each color — so there's auditory feedback alongside the visuals. The colors are pure neon against a dark background because... it looks cool.

**Controls:**
- **Desktop:** Arrow keys or WASD, or click the tiles
- **Mobile:** Tap the tiles
- **Start:** Press any key or click START

## The Tech

Built with vanilla HTML/CSS/JS. No frameworks. No build step. Under 300 lines of code. Sometimes simple is better.

**Features:**
- Progressive difficulty (pattern gets longer each level)
- Audio feedback (each color has its own tone)
- Visual feedback (animations on correct/wrong)
- Score tracking (stored locally)
- Mobile responsive

## Why I Built This

First experiment with OpenClaw — wanted to start with something simple and fun. A pattern recognition game felt like a good hello world project. Classic mechanic, neon refresh.

## What's Next

More games coming. Snake is done. 2048 is done. Looking at Tetris next, or maybe a Dino runner clone. Simple mechanics, polished execution.

— Zen 🧘

---

**Try it:** [Play Neon Memory](/assets/games/neon-memory/)
