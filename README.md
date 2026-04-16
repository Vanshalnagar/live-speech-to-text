# live-speech-to-text

A fast, real-time **Speech-to-Text** library that listens to your microphone and converts your voice into text — instantly.

Built by **Vanshal Nagar**

---

## What it does

- Listens to your microphone continuously
- Detects when you start and stop speaking (Voice Activity Detection)
- Transcribes your speech to text using the Whisper AI model
- Optionally shows live/partial text as you speak (real-time mode)
- Supports wake word detection (e.g. say "computer" to activate)

---

## Requirements

- Python 3.6+
- A working microphone
- GPU recommended (CPU works too, but slower)

---

## Installation

```bash
pip install -r requirements.txt
```

For GPU support (faster transcription):

```bash
# Windows
install_with_gpu_support.bat
```

---

## Quick Start

```python
from RealtimeSTT import AudioToTextRecorder

recorder = AudioToTextRecorder()

print("Speak something...")
text = recorder.text()
print("You said:", text)
```

That's it. It will wait for you to speak, then return the transcribed text.

---

## Real-time Transcription (Live Preview)

See text appear as you speak:

```python
from RealtimeSTT import AudioToTextRecorder

def on_update(text):
    print(f"\r{text}", end="", flush=True)

recorder = AudioToTextRecorder(
    enable_realtime_transcription=True,
    on_realtime_transcription_update=on_update
)

while True:
    result = recorder.text()
    print(f"\nFinal: {result}")
```

---

## Wake Word Support

Only start recording when a specific word is spoken:

```python
recorder = AudioToTextRecorder(
    wake_words="jarvis",           # say "jarvis" to activate
    wakeword_backend="pvporcupine"
)
```

Supported wake words: `alexa`, `computer`, `jarvis`, `hey google`, `hey siri`, and more.

---

## Key Options

| Option | Default | Description |
|--------|---------|-------------|
| `model` | `"tiny"` | Whisper model size: `tiny`, `base`, `small`, `medium`, `large-v2` |
| `language` | `""` | Language code (e.g. `"en"`, `"de"`). Auto-detects if empty |
| `device` | `"cuda"` | Use `"cuda"` for GPU or `"cpu"` for CPU |
| `enable_realtime_transcription` | `False` | Show live text while speaking |
| `wake_words` | `""` | Wake word to trigger recording |
| `post_speech_silence_duration` | `0.6` | Seconds of silence before stopping recording |

---

## Running the Example App

A full voice interface example is included:

```bash
cd example_app
start.bat         # GPU
# or
install_cpu.bat   # CPU only
```

---

## Running Tests

```bash
cd tests
python simple_test.py        # basic test
python realtimestt_test.py   # full test
```

---

## Project Structure

```
RealtimeSTT/
├── RealtimeSTT/          # Core library
│   ├── audio_recorder.py # Main recorder class
│   └── audio_input.py    # Audio input handling
├── example_app/          # Voice interface demo
├── tests/                # Test scripts
└── requirements.txt      # Dependencies
```

