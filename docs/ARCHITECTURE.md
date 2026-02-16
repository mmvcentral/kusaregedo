# Kusaregedo – System Architecture

This document provides a detailed analysis of the character's fight mode, skills, helpers, animations, and counter-party states.

---

## 1. Fight Mode Overview

### 1.1 Power Gauge System

| Variable | Purpose |
|----------|---------|
| `fvar(5)` | Power gauge value (0–1.18 or 1.02/1.18 depending on mode) |
| `fvar(6)` | Display scale (1.0 normal, 1.31 Pow-MAX, 1.51 Circumstance of Nothing) |
| `fvar(38)` | Super gauge value (used during Pow-MAX) |
| `fvar(39)` | Meditation gauge (0–125); used for Circumstance of Nothing |
| `var(38)` | Hit counter / special state (0–62 normal, 100 = Pow-MAX) |
| `var(39)` | Pow-MAX usage flag (0=available, 1=active, 2=used) |
| `var(37)` | Enables Circumstance of Nothing when losing |

**Gauge Display:**
- Life gauge position: `var(12)`, `var(13)` (X, Y)
- Power gauge position: `var(17)`, `var(18)` (X, Y)
- Helpers 7000 (life gauge) and 7500 (power gauge) display the bars

### 1.2 State Types

| State Type | Meaning |
|------------|---------|
| S | Standing |
| C | Crouching |
| A | Airborne |
| L | Lying down |
| H | Hit (throw/hitstun) |

### 1.3 Movement

- **Run**: State 100 (forward), State 105 (backward)
- **Walk**: State 20
- **Jump**: State 40 → 50
- **Air jump**: 0 (no air jump)
- **Meditation**: State 2100 (hold B to build fvar(39))

---

## 2. Skills by Category

### 2.1 Basic Arts (Standing)

| State | Name | Anim | Damage | Notes |
|-------|------|------|--------|------|
| 200 | Standing Light Punch | 200 | 64 | 3-hit combo (4,5,6) |
| 210 | Standing Medium Punch | 210 | 32 | High |
| 220 | Standing Heavy Punch | 220 | 152 | Slash helper 221 |
| 230 | Standing Heavy Punch (alt) | 230 | 136 | Slash helper 231 |
| 225 | Guard cancel | 225 | - | On guard |
| 240 | Standing Hard Punch | 240 | 112 | 3-hit (7,8,10) |
| 250 | Standing Hard Punch (close) | 250 | 360 | Close range |
| 245 | Guard cancel | 245 | - | On guard |
| 260 | Standing Kick | 260 | 64 | High |

### 2.2 Basic Arts (Crouching)

| State | Name | Anim | Damage | Notes |
|-------|------|------|--------|------|
| 400 | Crouching Light Punch | 400 | 24 | |
| 410 | Crouching Medium Punch | 400 | 24 | |
| 405 | Guard cancel | 405 | - | |
| 420 | Crouching Heavy Punch | 420 | 184 | Trip, slash helper 421 |
| 430 | Crouching Heavy Punch (alt) | 420 | 184 | Trip |
| 425 | Guard cancel | 425 | - | |
| 440 | Crouching Hard Punch | 440 | 272 | Fall |
| 450 | Crouching Hard Punch (alt) | 450 | 272 | Fall |
| 445 | Guard cancel | 445 | - | |
| 460 | Crouching Kick | 460 | 8 | |

### 2.3 Basic Arts (Air)

| State | Name | Anim | Damage | Notes |
|-------|------|------|--------|------|
| 300 | Run Light Punch | 300 | 32 | |
| 310 | Run Heavy Punch | 310 | 64 | Slash helper 311 |
| 320 | Run Hard Punch | 250 | 168 | Fall |
| 330 | Run Kick | 330 | 64 | |
| 600 | Air Light Punch | 600 | 64 | Slash helper 601 |
| 610 | Air Heavy Punch | 610 | 136 | Fall, juggle |
| 620 | Air Hard Punch | 620 | 272 | Fall, juggle |
| 630 | Air Kick | 630 | 112 | Fall |

### 2.4 Dir + Button

| State | Name | Command | Damage | Notes |
|-------|------|---------|--------|------|
| 700 | Down-Forward Kick | DF+Y | 64 | Trip |
| 710 | Forward Kick | F+Y | 64 | Jump-in attack |
| 500 | Low Down-Forward AY | DF+AY | 64 | Anti-air |
| 510 | High Down-Forward AY | DF+AY (air) | 152 | Anti-air |

### 2.5 Throws

| State | Name | Command | P1 State | P2 State |
|-------|------|---------|----------|----------|
| 800 | Forward Throw | F+Y | 810 | 820/821 |
| 850 | Backward Throw | B+Y | 860 | 870/871 |
| 900 | Throw follow-up | X or A (during throw) | - | - |

### 2.6 Special Arts

| State | Name | Command | Notes |
|-------|------|---------|-------|
| 1000 | Unko (糞) | ~DF,B,D,F,B,D,DB + AY | Projectile (proj 1000) |
| 1100 | Heretic's Throw (外道の投げ) | U+Y | Command throw |
| 1200 | Meat Lifter | B,D,DB + Y | Invincible |
| 1300 | Evil Spirit Summons (悪霊召喚) | D,DF,F + X or A | Helper 1300, projectile |
| 1400 | Gastrorrhea (逆流噴出) | D,DB,B + X or A | Projectile 1400 |

### 2.7 Super Arts

| State | Name | Command | Notes |
|-------|------|---------|-------|
| 3000 | Heretic Hunt (外道の連れ討ち) | U+Y+B or ~F,U,B,D | Command throw, requires Pow-MAX |
| 3100 | Flying Head Butt | D,DF,F + Y+B | Requires Pow-MAX |

### 2.8 Other Actions

| State | Name | Command | Notes |
|-------|------|---------|-------|
| 2000 | Forward Dash | DF+B | |
| 2010 | Backward Dash | DB+B | |
| 2020 | Crouch | D+B | |
| 2030 | Forward Jump | F+B | |
| 2040 | Back Jump | B+B | |
| 2100 | Meditation | D,DB,B,F + B or B hold | Builds fvar(39) |
| 2200 | Power Defense | D,DB,B,F + B | Reversal |
| 2300 | Recovery (AY) | A+Y | |
| 2400 | Pow-MAX | X+Y+A | Activates helper 7510 |
| 2500 | Suicide | B,F,D + S | Instant death |
| 3500 | Issen (一閃) | Y+A+B | When Circumstance of Nothing active |

### 2.9 Circumstance of Nothing (無の境地)

| State | Command | Notes |
|-------|---------|-------|
| 7550 | D,DB,B + Y+B | When `floor(fvar(39)*8) >= life` and var(37) |

---

## 3. Helpers and Effects

### 3.1 Blood Effects

| Helper ID | State | Name | When |
|-----------|-------|------|------|
| 8100 | 8100 | blood_ss | Large hit (var(48)=0) |
| 8110 | 8110 | blood_s | Small hit (var(48)=1) |
| 8120 | 8120 | blood_m | Medium (var(48)=2, type 1) |
| 8121 | 8121 | blood_m | Medium (var(48)=2, type 2) |
| 8130 | 8130 | blood_l | Large (var(48)=3, type 1) |
| 8131 | 8131 | blood_l | Large (var(48)=3, type 2) |
| 8132 | 8132 | blood_l | Large (var(48)=3, type 3) |
| 8140 | 8140 | blood_issen | Issen super finish |

### 3.2 Slash Effects

| Helper ID | State | Parent State |
|-----------|-------|--------------|
| 221 | 221 | 220 |
| 231 | 231 | 230 |
| 241 | 241 | 240, 3510 |
| 421 | 421 | 420, 430 |
| 601 | 601 | 600 |
| 311 | 231 | 310 |

### 3.3 Guard Effect

| Helper ID | State | When |
|-----------|-------|------|
| 8020 | 8020 | Move guarded |

### 3.4 Gauge Helpers

| Helper ID | State | Purpose |
|-----------|-------|---------|
| 7000 | 7000 | Life gauge display |
| 7500 | 7500 | Power gauge display |
| 7510 | 7510 | Pow-MAX mode helper |
| 7550 | 7550 | Circumstance of Nothing |

### 3.5 Counter Hit Display

| Helper ID | State | When |
|-----------|-------|------|
| 8899–8907 | 8900 | Counter hit (var(34)) |

### 3.6 Projectiles

| Proj ID | Parent | Damage |
|---------|--------|--------|
| 1000 | 1000 | 136 |
| 1300 | 1305 | 64 |
| 1400 | 1400 | 24,8 |
| 3150 | 3150 | - |
| 3156 | 3150 | 344 (Issen) |

---

## 4. Animations and Counter-Parties

### 4.1 Throw Victim States

| P2 State | Animation | When |
|----------|-----------|------|
| 820 | 820 | Forward throw victim (standing) |
| 821 | 821 | Forward throw victim (fall) |
| 870 | 870 | Backward throw victim (standing) |
| 871 | 871 | Backward throw victim (fall) |
| 1120 | 1120 | Heretic's throw victim (air) |
| 1121 | 1121 | Heretic's throw victim (fall) |
| 3021 | 3021 | Heretic Hunt victim (air) |
| 3060 | 3060 | Heretic Hunt victim (carry) |
| 3061 | 3061 | Heretic Hunt victim (fall) |
| 3520 | 3520 | Issen victim (hit) |
| 3521 | 3521 | Issen victim (fall) |

### 4.2 Projectile Hit States

| State | When |
|------|------|
| 1310 | Evil Spirit hit |
| 1311 | Evil Spirit hit (fall) |
| 1410 | Gastrorrhea hit (normal) |
| 1411 | Gastrorrhea hit (recovery) |
| 1420 | Gastrorrhea hit (trip) |
| 1421 | Gastrorrhea hit (fall) |

### 4.3 Power Defense

| State | When |
|------|------|
| 2210 | Power Defense victim (hit) |
| 2211 | Power Defense victim (recovery) |

### 4.4 Hit Stun

Standard hit states use 5002, 5007, 5012, 5017, 5030, 5050, etc. via `authorname` checks for compatibility with different common states.

---

## 5. Config File (config.txt)

| State | Purpose |
|-------|---------|
| 5900 | Round initialization |

**Config Variables:**

- `fvar(39)` = 5: Power gauge initial value
- `var(20)` = 20: Display time for special/super command display
- `var(12)`, `var(13)` = Life gauge position (141, 32)
- `var(17)`, `var(18)` = Power gauge position (91, 229)

---

## 6. AI

- **State 10000**: AI helper; processes commands and triggers
- **State 1**: CPU helper (SSV-Helper.cns)
- **Var(45)**: 0 = player, 1 = CPU
- **Var(44)**: AI trigger flag

---

## 7. Variable Reference (kusaregedo-N.cns)

| Var | Purpose |
|-----|---------|
| 1 | Combo counter (body) |
| 2 | Hit sound index |
| 3 | Guard sound index |
| 4 | Combo counter (throw) |
| 5 | Gastrorrhea hit type |
| 6 | Power gauge target |
| 7 | Command power modifier |
| 8 | Command power modifier 2 |
| 10 | Recovery target |
| 11 | Air dash direction |
| 12–13 | Life gauge position |
| 14 | Issen damage |
| 15 | Power gauge display |
| 16 | Power gauge fill |
| 17–18 | Power gauge position |
| 19 | Fall type |
| 20 | Command display time |
| 37 | Circumstance of Nothing enable |
| 38 | Hit counter / special state |
| 39 | Pow-MAX usage |
| 44 | AI trigger |
| 45 | CPU flag |
| 46 | Spark Y offset |
| 47 | Spark type |
| 48 | Combo type (blood effect) |

| FVar | Purpose |
|------|---------|
| 5 | Power gauge value |
| 6 | Display scale |
| 38 | Super gauge |
| 39 | Meditation gauge |
