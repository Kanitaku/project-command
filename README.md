[Commandreadme.txt](https://github.com/user-attachments/files/28920753/Commandreadme.txt)# project-command
A fully local offline AI desktop companion: voice, memory, emotion, and games. Built with Python and Ollama.


> A fully local, offline AI desktop companion — voice, memory, emotion, and games. No subscriptions. No cloud. No limits.

![Python](https://img.shields.io/badge/Python-3.11-blue?style=flat-square&logo=python)
![Ollama](https://img.shields.io/badge/LLM-Ollama-black?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?style=flat-square&logo=windows)
![Status](https://img.shields.io/badge/Status-Active%20Development-green?style=flat-square)
![License](https://img.shields.io/badge/License-Personal%20Use-orange?style=flat-square)

---

## What Is This?

**Project Command** is a feature-complete local AI companion application built entirely in Python with a free, open-source stack. No API keys. No monthly fees. No internet connection required after setup.

Command is a kuudere combat android character who listens to your voice, thinks with a local LLM, and speaks back using a realistic text-to-speech engine. She remembers your conversations, tracks your mood, and reacts emotionally — all running privately on your own hardware.

Built from scratch by a self-taught developer using AI-assisted coding. Every feature documented, every decision intentional.

---

## Features

### Core Experience
- **Voice conversation** — speak naturally using LEFT CTRL push-to-talk or auto-listen mode with VAD silence trimming
- **Local LLM brain** — powered by `fluffy/l3-8b-stheno-v3.2` via Ollama, fully offline
- **Realistic TTS** — Kokoro ONNX (`af_bella` voice) for natural speech output
- **Speech-to-text** — Faster Whisper (small model, CUDA accelerated)
- **Interrupt/stop** — cancel speech mid-sentence at any time

### Memory System
- **Persistent SQLite memory** — facts, mood, milestones, and plans saved across sessions
- **Two-stage extraction** — fast regex Stage 1 + async LLM Stage 2 for deep fact capture
- **Session summaries** — Command remembers what happened last time
- **Time-aware greetings** — she knows if you've been gone for minutes, hours, or days
- **Mood detection** — detects stress, sadness, happiness in your messages and shifts her tone accordingly
- **Milestone tracking** — meaningful moments acknowledged (not frivolous counters)
- **Plans/promises** — catches future intentions and brings them back up naturally

### Character & Emotion
- **Emotion-reactive portrait system** — 6 emotion states with smooth transitions
- **Breathing and blinking animation** — subtle life in every idle moment
- **Three costume sets** — Civilian, Combat, Swimsuit, each with full emotion portrait sets
- **Intimacy escalation ladder** — personality deepens with persistence, not randomly
- **Single source of truth config** — all personality and costume data in `command_config.py`

### Visual Modes
- **Full Interface** (`main.py`) — portrait panel + chat log + controls
- **Desktop Mate** (`desktop_mate.py`) — transparent floating PNG, draggable, resizable, subtitles
- **Full Window Mode** (`fullwindow.py`) — fullscreen on second monitor, static background

### Nine Minigames
| Game | File |
|------|------|
| Strip RPS (with emotional reactions) | `StripRPS_1.py` |
| War Games Tic-Tac-Toe | `Wargamesrps.py` |
| Hangman | `Hangman.py` |
| Kanji Match | `Kanjimatch.py` |
| Blackjack | `Blackjack.py` |
| Strip Battleship | `Battleship.py` |
| LLM-powered Trivia | `Trivia.py` |
| Breakout | `Breakout.py` |
| Affection Clicker + Eternity Mode | `Clicker.py` |

### Standalone Panels
- **Japanese Study Panel** — vocabulary and Kanji practice with Command
- **VIP Art Gallery** — unlock-gated gallery with music and easter eggs

### Launcher (`launcher.py`)
- Matrix boot sequence
- System health checks
- Costume selection with preview and voice line
- Idle voice lines and background music
- Command history export, trim, and wipe utilities
- Game progress tracking and reset

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Python 3.11 (conda env) |
| LLM Runtime | Ollama (local) |
| LLM Model | fluffy/l3-8b-stheno-v3.2 |
| Text-to-Speech | Kokoro ONNX |
| Speech-to-Text | Faster Whisper (CUDA) |
| Voice Activity Detection | Silero VAD |
| Memory/Storage | SQLite via `command_memory.db` |
| UI Framework | Tkinter |
| Audio | sounddevice, pygame |
| System Tray | pystray |
| GPU | NVIDIA GeForce RTX 5060 Ti (16GB VRAM, CUDA 13.2) |
| OS | Windows |

---

## Project Structure

```
ai_waifu_project/
│
├── launcher.py              # Main entry point — Matrix boot, mode selection
├── main.py                  # Full Interface mode
├── desktop_mate.py          # Floating desktop companion mode
├── fullwindow.py            # Fullscreen mode (monitor 2)
├── command_config.py        # BASE_SYSTEM_PROMPT + COSTUMES (single source of truth)
├── memory.py                # Full memory system (SQLite, extraction, summaries)
│
├── ArtGallery.py            # VIP art gallery panel
├── JapaneseStudy.py         # Japanese study panel
├── Datemode.py              # Date Mode visual novel (in development)
│
├── Clicker.py               # Affection Clicker + Eternity Mode
├── Battleship.py            # Strip Battleship
├── StripRPS_1.py            # Strip Rock Paper Scissors
├── Wargamesrps.py           # War Games Tic-Tac-Toe
├── Hangman.py               # Hangman
├── Kanjimatch.py            # Kanji Match
├── Blackjack.py             # Blackjack
├── Trivia.py                # LLM-powered Trivia
├── Breakout.py              # Breakout
│
├── Command.Modelfile        # Ollama model configuration
├── command_memory.db        # SQLite memory database (generated on first run)
├── selected_costume.json    # Active costume state
├── command_progress.json    # Game progress and unlock tracking
└── Launch_Command.bat       # Launch script (in progress)
```

---

## Requirements

### Hardware
- NVIDIA GPU with CUDA support recommended (16GB VRAM tested)
- CPU inference possible but significantly slower for voice response

### Software Prerequisites

Install these before running the project:

1. **Ollama** — [ollama.com](https://ollama.com) — local LLM runtime
2. **Conda** — for Python environment management
3. **CUDA Toolkit** — matching your GPU driver

### Python Dependencies

```bash
conda create -n ai_waifu_env python=3.11
conda activate ai_waifu_env
pip install faster-whisper kokoro-onnx sounddevice pygame pystray pillow
```

### Pull the LLM Model

```bash
ollama pull fluffy/l3-8b-stheno-v3.2
ollama create command -f Command.Modelfile
```

---

## Setup & Launch

```bash
# 1. Activate environment
conda activate ai_waifu_env

# 2. Start Ollama (if not already running)
ollama serve

# 3. Launch Project Command
python launcher.py
```

From the launcher you can select your visual mode, choose a costume, and enter the companion experience.

---

## Development Notes

This project was built using AI-assisted development (Claude API) by a self-taught developer with no formal CS background. It represents a complete, working application built from lived curiosity and disciplined iteration.

**What I learned building this:**
- Local LLM integration and model configuration via Ollama Modelfiles
- Custom TTS/STT pipeline design (Kokoro + Faster Whisper + Silero VAD)
- SQLite database architecture for persistent AI memory
- Multi-module Python application design
- Emotion state management and animation systems in Tkinter
- VRAM optimization for consumer GPU inference

---

## Roadmap

- [ ] One-click `.bat` launcher polish
- [ ] Fact-driven proactive dialogue (unprompted check-ins)
- [ ] Game outcome emotional feedback system
- [ ] Date Mode visual novel (in separate development branch)
- [ ] Brain fine-tuning with Unsloth/Axolotl on conversation logs
- [ ] Voice cloning with XTTS (pending driver compatibility)
- [ ] Discord bot integration (stretch goal)

---

## About

Built by **Kanitaku** — documenting the full journey of building AI from zero.

- 📺 YouTube: [youtube.com/@Kanitakubuilder](https://youtube.com/@Kanitakubuilder)
- 🐦 X/Twitter: [@Kanitakubuilder](https://x.com/Kanitakubuilder)

---

*Project Command is a personal portfolio project. All AI-generated assets are for personal/portfolio use.*
