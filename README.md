# Kusaregedo (腐れ外道)

A M.U.G.E.N character based on **Kusaregedo** from *Samurai Shodown V* / *Samurai Spirits Zero* (サムライスピリッツ零).

---

## Table of Contents

1. [Character Introduction](#character-introduction)
2. [Original Creator & Credits](#original-creator--credits)
3. [Character Storyline](#character-storyline)
4. [File Structure](#file-structure)
5. [System Architecture](#system-architecture)
6. [Document Index](#document-index)
7. [License](#license)

---

## Character Introduction

| Property | Value |
|----------|-------|
| **Display Name** | Kusaregedo |
| **Full Name** | Kusaregedo (腐れ外道, "Rotten Heretic") |
| **Source** | Samurai Shodown V / Samurai Spirits Zero |
| **M.U.G.E.N Version** | 04,14,2002 |
| **Character Version** | 1.04 |

**Kusaregedo** is a grotesque, otherworldly fighter from the Samurai Shodown series. His name means "Rotten Heretic" or "Corrupt Villain." He fights with unorthodox techniques including projectile attacks, throws, and a unique meditation/power gauge system. The character features a Pow-MAX mode, special moves such as Evil Spirit Summons and Gastrorrhea, and super arts including Heretic Hunt and Flying Head Butt.

---

## Original Creator & Credits

| Role | Name |
|------|------|
| **Original Creator** | H" (H-h) |
| **Contact** | ms09dom61@hotmail.com |

The character was created for M.U.G.E.N by H". Configuration options (including power gauge display) can be adjusted in `config.txt`.

---

## Character Storyline

Kusaregedo is a mysterious entity from the Samurai Shodown universe. His backstory suggests he became "rotten" (腐れ) when his heart was attached to him. He embodies the path of Shura (修羅の道) and fights with grotesque, unsettling techniques. His moveset includes vomiting projectiles, summoning evil spirits, and performing brutal throws. The character is designed to be disturbing and unconventional, fitting his role as a "heretic" in the series.

---

## File Structure

```
kusaregedo/
├── kusaregedo.def        # Main character definition
├── kusaregedo.cmd        # Command definitions & state triggers
├── kusaregedo-N.cns      # Normal states (constants, basic arts)
├── kusaregedo-S.cns      # Special arts states
├── kusaregedo-H.cns      # Super arts states
├── SSV-Helper.cns        # Helper states (blood effects, gauges, etc.)
├── config.txt            # Round initialization & config (power gauge, etc.)
├── kusaregedo.air        # Animation data
├── skill.htm             # Skill/move list (Japanese)
├── skill/skill.htm       # Skill reference copy
└── docs/                 # Documentation
    ├── ARCHITECTURE.md   # System architecture, skills, animations
    ├── TRANSLATION.md    # Japanese comment translations
    └── log.md            # Creator history & changelog
```

---

## System Architecture

*For detailed analysis of fight mode, skills, helpers, animations, and counter-party states, see [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).*

### Overview

- **Power Gauge**: Uses a custom gauge (fvar(39)) that can be filled via meditation and attacks. Pow-MAX mode (XYA) activates when gauge is full.
- **Special Moves**: Evil Spirit Summons, Gastrorrhea, Heretic Brand, Meat Lifter, Power Defense, Circumstance of Nothing (Mu no kyouti), Suicide.
- **Super Arts**: Heretic Hunt, Flying Head Butt.
- **Throws**: Forward and backward throws with combo follow-ups.
- **Helpers**: Blood effects (small, medium, large), guard effects, counter-hit display, power gauge display.

---

## Document Index

### Documentation

| Document | Path | Description |
|----------|------|-------------|
| README | `README.md` | This file – overview and reference |
| **Architecture** | [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | System architecture, skills, animations |
| **Translation** | [docs/TRANSLATION.md](docs/TRANSLATION.md) | Japanese comment translations |
| **Log** | [docs/log.md](docs/log.md) | Creator history, changelog |

### Character Files

| Document | Path | Description |
|----------|------|-------------|
| Character Definition | `kusaregedo.def` | Def file, palettes, file refs |
| Commands | `kusaregedo.cmd` | Inputs and state triggers |
| Normal CNS | `kusaregedo-N.cns` | Basic arts, movement, throws |
| Special CNS | `kusaregedo-S.cns` | Special move states |
| Super CNS | `kusaregedo-H.cns` | Super art states |
| Helper CNS | `SSV-Helper.cns` | Helpers, gauges, effects |
| Config | `config.txt` | Round init, power gauge settings |
| Animations | `kusaregedo.air` | Animation definitions |
| Skill Reference | `skill.htm` | Move list |

---

## License

**Creative Circle License**

This M.U.G.E.N character is a fan-made derivative work based on **Kusaregedo** from *Samurai Shodown V* / *Samurai Spirits Zero*.

- **Original character**: © SNK / SNK Playmore
- **M.U.G.E.N character**: © H" (original creator)
- **Edition**: This documentation and organization is an edition from the original author's release.

This work is intended for non-commercial, personal use within the M.U.G.E.N community. Do not redistribute for profit. Respect the original creator's terms and the intellectual property of the source material.
