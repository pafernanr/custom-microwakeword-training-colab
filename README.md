# Custom microWakeWord Training (Colab)

Turnkey Google Colab notebook for training custom [microWakeWord](https://github.com/kahrendt/microWakeWord) wake words. Produces TensorFlow Lite models that run on ESP32 microcontrollers via [ESPHome](https://esphome.io/).

This is **not** a fork of microWakeWord — it's an end-to-end wrapper that installs it as a dependency and adds:

- **Automated sample generation** via [Piper TTS](https://github.com/rhasspy/piper) — no need to record your own audio
- **Automated dataset downloads** — augmentation data (MIT RIRs, AudioSet, FMA) and negative examples, all wired up
- **Interactive pronunciation testing** — listen to TTS variants and select the best ones before training
- **Single CONFIG dict** — abstracts away YAML configs, CLI flags, and directory plumbing
- **Built-in bug workarounds** — stride assertion patch, datasets version pinning, OOM avoidance on free-tier Colab

## Pre-trained wake words

The `wakewords/` directory includes two ready-to-use Spanish wake words:

| Wake word | Language | Model |
|-----------|----------|-------|
| Gertrudis | es | `wakewords/gertrudis/gertrudis.tflite` |
| Hey Charo | es | `wakewords/hey_charo/hey_charo.tflite` |

## Quick start

1. Open the notebook in Google Colab (Runtime > Change runtime type > **T4 GPU**)
2. Edit the `CONFIG` dictionary in Cell 1 — set your wake word name, language, pronunciation variants, and clip duration
3. Run cells sequentially — Cell 5 plays audio samples so you can pick the best pronunciation variants
4. After training (~20 min on T4), download the `.tflite` model

## Notebook workflow

| Cell | Step |
|------|------|
| 1 | Configuration (wake word name, language, training params) |
| 2 | Install dependencies (`microWakeWord`, `piper-tts`, `datasets`) |
| 3 | Patch microWakeWord stride assertion bug |
| 4 | Download Piper TTS voice models for your language |
| 5 | Test pronunciation variants (listen and select) |
| 6 | Generate training samples via Piper TTS |
| 7 | Download augmentation data (MIT RIRs, AudioSet, FMA) |
| 8 | Generate augmented spectrogram features |
| 9 | Download negative example datasets |
| 10 | Build training YAML config |
| 11 | Train MixedNet model |
| 12 | Download `.tflite` model |

## Configuration

Key parameters in the `CONFIG` dictionary:

- `WAKE_WORD_NAME` — output directory and model name
- `CLIP_DURATION_MS` — `1500` for single words, `1800` for two-word phrases
- `TEST_VARIANTS` — pronunciation variants to test (e.g., `['gertrudis', 'gertru-dis']`)
- `LANGUAGE` / `VOICE_QUALITY` — Piper TTS language code and quality level
- `TRAINING_STEPS` — default `10000`, more steps may improve accuracy
- `NEGATIVE_CLASS_WEIGHT` — increase to reduce false positives (default `20`)

## ESPHome deployment

Copy the `.tflite` model and its `.json` manifest to your ESPHome config. Example ESPHome YAML:

```yaml
micro_wake_word:
  models:
    - model: gertrudis.tflite
      probability_cutoff: 0.85
      sliding_window_size: 5
  on_wake_word_detected:
    - voice_assistant.start:
```

Requires ESPHome 2024.7.0 or later.

## Credits

- [microWakeWord](https://github.com/kahrendt/microWakeWord) by Kevin Ahrendt
- [Piper TTS](https://github.com/rhasspy/piper) by Rhasspy
- [ESPHome](https://esphome.io/)
