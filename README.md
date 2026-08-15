# 🎵 LYRICODE 
**Turn any song into an ESP32 OLED Lyric Visualizer using AI.**

Stop guessing timestamps. LYRICODE is an end-to-end Python pipeline that takes an `.mp3` and a `.txt` file, isolates the vocals, aligns every single word to the exact millisecond, and generates a ready-to-flash Arduino `.ino` file. 

![Demo GIF Placeholder](https://via.placeholder.com/800x400.png?text=Add+Your+OLED+Demo+GIF+Here!)

## ✨ Why it's awesome
* 🤖 **AI-Powered:** Uses Meta's **Demucs** (vocal isolation), **WhisperX** (forced alignment), and **Librosa** (DSP audio snapping).
* ✂️ **Smart Auto-Trim:** Automatically cuts songs longer than 90 seconds and trims the lyrics to match.
* 🔥 **Fire Mode:** Detects non-English lyrics (Japanese, Hindi, etc.) and instantly generates a pure audio-visualizer mode with a flickering fire animation.
* 🎛️ **Live Nudge:** Drifted by 0.5s? Just TAP or HOLD the ESP32's BOOT button while the song plays to fix the sync on the fly.
* 🎨 **4 Animation Themes:** Energy (Tunnel/EQ), Chill (Stars), Glitch (Matrix), and Dreamy (Bubbles).

## 🔌 Hardware Required
* **ESP32** Dev Board
* **0.96" SSD1306 OLED** (I2C)
* **4 Jumper Wires** (VCC ➔ 3.3V, GND ➔ GND, SCL ➔ GPIO22, SDA ➔ GPIO21)

## 🚀 Quick Start (The 1-Command Magic)

**1. Install dependencies:**
```bash
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu118 && pip install demucs librosa soundfile numpy whisperx faster-whisper
```

**2. Drop your files:**
Put your `song.mp3` and `lyrics.txt` in the project folder.

**3. Run the pipeline:**
```bash
python lyricode.py
```
*The script will clean the cache, decode the audio, refine the timestamps, suggest an animation theme based on the song's BPM, and output your custom `.ino` file into a dedicated subfolder.*

**4. Flash & Play:**
Open the generated `.ino` in Arduino IDE, upload it to your ESP32, press play on your phone, and hit the BOOT button on the first word!

## 📂 Project Structure
```text
LYRICODE/
├── lyricode.py        # 🪄 The 1-command master pipeline
├── core.py            # 🧠 AI Engine (Demucs + VAD + WhisperX)
├── refine.py          # 🎯 DSP onset snapping
├── main.py            # ⚙️ Manual CLI decoder
└── songs/             # 📁 Auto-generated output folders
```

## 🛠️ Troubleshooting
* **Used the wrong song's vocals?** Run `rmdir /s /q stems` to clear the cache.
* **Arduino `drawVLine` error?** The script auto-patches this, but ensure you have the latest `Adafruit GFX` library installed.
* **Words switching too fast?** The `refine.py` script holds words until the next vocal onset. Ensure your `lyrics.txt` matches the actual words sung!

## 🙏 Built With
[Demucs](https://github.com/facebookresearch/demucs) • [WhisperX](https://github.com/m-bain/whisperX) • [Silero VAD](https://github.com/snakers4/silero-vad) • [Librosa](https://librosa.org/) • [Adafruit GFX](https://github.com/adafruit/Adafruit-GFX-Library)

**License:** MIT - Free to use, modify, and share. Built with ❤️ for the maker community.
