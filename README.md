[readme.md](https://github.com/user-attachments/files/23562473/readme.md)
# AI Rhythm — Python ("Kimi")

A Python-based rhythm engine that recreates osu!-style hitobjects (circles, sliders, long notes) and uses “Kimi,” an AI player that reads objects, predicts timing, and follows slider paths using Bezier/Catmull curves. Supports both JSON beatmaps. Designed for learning, experimentation, and AI development—NOT for cheating.

---

## Table of Contents

- [Project goals](#project-goals)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [How Kimi (the AI) is used](#how-kimi-the-ai-is-used)
- [Development notes](#development-notes)
- [Contributing](#contributing)
- [Known issues & roadmap](#known-issues--roadmap)
- [License](#license)
- [Credits](#credits)

---

## Project goals

The aim of this project is to provide:

- A playable rhythm experience with accurate audio sync.
- Programmatic generation and editing of beatmaps using a lightweight AI assistant (Kimi).
- Support for advanced note types: sliders, long notes, spinners (or equivalent), and hold notes.
- Clean, modular code so the project can be extended into a full GitHub repo and packaged.

## Features

- Audio playback and precise timing / sync system.
- Note types: regular notes, sliders, long/hold notes.
- Visual UI elements: playfield, combo counter, hit feedback, judgement display.
- AI assistant (Kimi) that can generate suggested hit timings / difficulty adjustments from audio analysis.
- Export / import of beatmaps in a simple JSON format (easy to convert to osu! or other formats).
- CLI tools for batch-processing audio files to generate raw timing tracks.



````


## Requirements

This project targets Python 3.10+. Typical dependencies (example):

- `numpy` — numeric operations
- `sounddevice` or `pydub` / `pygame` — audio playback & processing
- `librosa` — audio analysis (beat detection) *optional*
- `pygame` or `pyglet` — rendering & input
- `pytest` — tests

> See `requirements.txt` for a pinned list included in the repo.


## Installation

1. Clone the repository (or unzip the provided package):

```bash
git clone https://github.com/<your-user>/ai-rhythm-kimi.git
cd ai-rhythm-kimi
````

2. Create a virtual environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / macOS
.venv\Scripts\activate     # Windows
pip install -r requirements.txt
```

3. (Optional) Install development extras:

```bash
pip install -r dev-requirements.txt
```

## Usage

Start the game/player (example):

```bash
python src/main.py --map examples/example_map.json --audio assets/song.mp3
```

Common CLI flags (example):

- `--map` — path to beatmap JSON file.
- `--audio` — path to audio file (mp3/wav).
- `--difficulty` — difficulty preset (easy/normal/hard).
- `--headless` — run audio analysis without rendering (for batch generation).

### Generating a beatmap with Kimi (AI)

```bash
python src/ai_kimi/generate.py --audio assets/song.mp3 --out examples/generated_map.json --mode auto
```

`generate.py` will run a beat detection pass, propose note timings, and annotate sliders/long notes heuristically.

## Configuration

Settings can live in a `config.yaml` or `settings.json` (example fields):

```yaml
hit_windows:
  perfect: 30   # milliseconds
  great: 60
  good: 100
  miss: 150
audio:
  buffer_size_ms: 100
ui:
  resolution: [1280, 720]
  fullscreen: false
```

## How Kimi (the AI) is used

Kimi is implemented as a set of deterministic processing steps + optional ML models:

1. **Onset detection** — find likely hit times from the audio waveform.
2. **Beat / tempo extraction** — estimate BPM and time signature.
3. **Note grouping** — cluster onsets into notes, sliders, and long notes.
4. **Difficulty shaping** — place extra notes or reduce density depending on chosen difficulty.

Kimi's outputs are suggestions — you can edit exported JSON maps manually in the `examples/` folder.

## Development notes

- Keep audio timing code as the single source of truth: all rendering and hit detection should reference the exact playback position.
- Aim for deterministic behavior: use fixed random seeds in the AI generator when `--seed` is provided.
- Use a modular renderer so the UI can be swapped (SDL/Pygame, OpenGL, or web frontend later).

## Contributing

Contributions are welcome! Suggested workflow:

1. Fork the repository.
2. Create a branch: `git checkout -b feat/your-feature`.
3. Add tests for new functionality.
4. Open a pull request with a clear description.

Please follow the coding style and keep commits small and focused.

## License

MIT License

```
MIT License

Copyright (c) 2025 Your Name

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Credits

- Project lead / initial author: z1bf
- AI assistant (project codename): **Kimi**
- Libraries: `librosa`, `numpy`, `pygame` (or alternatives)

---


