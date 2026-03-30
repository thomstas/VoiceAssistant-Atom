# 🚀 Branch: Custom Wake Word Training

This branch is dedicated to training and implementing a **personalized wake word** for the M5Stack Atom Echo using the `micro_wake_word` engine.

## 🎤 Phase 1: Recording Your Voice
To train a high-quality model, you need to provide the AI with diverse samples of your voice recorded in the target environment.

### Recording Requirements:
* **Format**: `.wav` (PCM)
* **Sample Rate**: `16000 Hz` (16kHz)
* **Channels**: `Mono`
* **Bit Depth**: `16-bit`

### Data Collection Strategy:
1.  **Quantity**: Aim for **40-60 samples** of your chosen wake word.
2.  **Diversity**: 
    * Record at different times of the day.
    * Vary your distance (0.5m, 2m, 5m).
    * Vary your tone (whisper, normal, loud).
3.  **Environment**: Record in the same room where the Atom Echo is installed to capture the local acoustics.

---

## 🧠 Phase 2: Training the Model (Google Colab)
We use Google's cloud infrastructure to train the TensorFlow Lite model.

1.  **Open the Notebook**: [micro_wake_word Training Colab](https://colab.research.google.com/github/esphome/micro-wake-word/blob/main/notebooks/train_micro_wake_word.ipynb).
2.  **Upload Samples**: Put all your `.wav` files into a folder named after your wake word and upload it to the Colab environment (or link your Google Drive).
3.  **Run Training**: Follow the steps in the notebook to generate your `.tflite` file.

---

## 🛠️ Phase 3: Deployment to ESPHome
Once you have your `model_name.tflite` file:

1.  **Upload**: Place the file in `/config/esphome/VoiceAssistant/my_echo/`.
2.  **Update `voice.yaml`**:
    Change the model path to point to your new file:
    ```yaml
    micro_wake_word:
      models:
        - url: [https://github.com/esphome/micro-wake-word-models/raw/main/models/alexa.tflite](https://github.com/esphome/micro-wake-word-models/raw/main/models/alexa.tflite) # Keep as fallback
        - file: my_custom_word.tflite # Your new model
    ```
3.  **Compile & Flash**: Re-install the firmware and test!

---

## ⚠️ Notes for the `custom-wake-word` Branch
* Expect **RAM usage** to be tight. If the device crashes, ensure `codec_support_enabled: false` is set in `audio.yaml`.
* If the model is too sensitive (false triggers), increase the `probability_cutoff` in the `voice_assistant` configuration.
