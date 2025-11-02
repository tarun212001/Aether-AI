# 🎙️ Aether AI Voice Chat  

> **Talk to your AI — privately, locally, and in real time.**  
> A fully offline, customizable voice-based chatbot powered by open-source AI models.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)
![License](https://img.shields.io/badge/License-Coqui%20Public%20Model%20License%201.0.0-green.svg)
![Status](https://img.shields.io/badge/Status-Alpha-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)
![GPU](https://img.shields.io/badge/GPU-8GB%2B%20VRAM%20Recommended-blueviolet.svg)

---

## 🧠 About the Project

** Aether AI Voice Chat** brings together cutting-edge open-source AI tools to let you **converse naturally with your computer — completely offline.**

It integrates the **Zephyr 7B** language model with real-time **speech-to-text** and **text-to-speech** components, enabling fast, natural, and secure voice-based interactions on your local machine.

This is a demonstration of how real-time transcription, local inference, and custom voice synthesis can create a powerful conversational AI without the need for cloud services.

---

## 🧩 Tech Stack

| Component | Technology | Description |
|------------|-------------|-------------|
| **Language Model** | [llama.cpp](https://github.com/ggerganov/llama.cpp) + **Zephyr 7B** | Lightweight LLM inference for local chat |
| **Speech-to-Text (STT)** | [RealtimeSTT](https://github.com/KoljaB/RealtimeSTT) + **faster_whisper** | High-speed, low-latency voice transcription |
| **Text-to-Speech (TTS)** | [RealtimeTTS](https://github.com/KoljaB/RealtimeTTS) + **Coqui XTTS** | Real-time natural voice synthesis |

---

## ⚠️ Project Status  

🚧 **Experimental Alpha Build**  

This project is in early development and **not yet production-ready.**  
While it delivers solid performance for a 7B model, you may experience:
- Occasional **voice glitches** with XTTS 2.0  
- **Latency** on lower-end GPUs  
- **Simpler reasoning** compared to GPT-4 or Claude  

Please consider this a proof-of-concept for a local, private, real-time AI voice assistant.

---

## 🆕 Updates  

- 🔊 Updated to **Coqui XTTS 2.0** for improved synthesis quality  
- 🐞 Fixed RealtimeTTS model download bug  
- ⚙️ Stability and dependency improvements  

---

## 💻 Prerequisites  

### 🖥️ Hardware
- GPU with **at least 8 GB VRAM** recommended for real-time performance  

### ⚙️ Software  

#### For NVIDIA Users
- **CUDA Toolkit 11.8** → [Download](https://developer.nvidia.com/cuda-11-8-0-download-archive)
- **cuDNN 8.7.0 for CUDA 11.x** → [Download](https://developer.nvidia.com/rdp/cudnn-archive)

#### For AMD Users
- **ROCm SDK 5.7.1** → [Download](https://www.amd.com/en/developer/resources/rocm-hub/hip-sdk.html)

#### FFmpeg
Install FFmpeg according to your OS:

```bash
# Ubuntu / Debian
sudo apt update && sudo apt install ffmpeg

# Arch Linux
sudo pacman -S ffmpeg

# macOS (Homebrew)
brew install ffmpeg

# Windows (Chocolatey)
choco install ffmpeg

# Windows (Scoop)
scoop install ffmpeg


### Installation Steps 

1. Clone the repository or download the source code package.

2. Install llama.cpp
    - (for AMD users) Before the next step set env variable `LLAMA_HIPBLAS` value to `on`

    - Official way:
     ```python
     pip install llama-cpp-python --force-reinstall --upgrade --no-cache-dir --verbose
     ```

    - If the official installation does not work for you, please install [text-generation-webui](https://github.com/oobabooga/text-generation-webui), which provides some excellent wheels for a lot of platforms and environments

3. Install realtime libraries
   - Install the main libraries:
     ```python
     pip install RealtimeSTT==0.1.7
     pip install RealtimeTTS==0.2.7
     ```
4. Download zephyr-7b-beta.Q5_K_M.gguf from [here](https://huggingface.co/TheBloke/zephyr-7B-beta-GGUF/tree/main). 
   - Open creation_params.json and enter the filepath to the downloaded model into `model_path`.
   - Adjust n_gpu_layers (0-35, raise if you have more VRAM) and n_threads (number of CPU threads, i recommend not using all available cores but leave some for TTS)

5. If dependency conflicts occur, install specific versions of conflicting libraries:
     ```python
     pip install networkx==2.8.8
     pip install typing_extensions==4.8.0
     pip install fsspec==2023.6.0
     pip install imageio==2.31.6
     pip install numpy==1.24.3
     pip install requests==2.31.0
     ```   

## Running the Application
     python ai_voicetalk_local.py

## Customize

### Change AI personality

Open chat_params.json to change the talk scenario.

### Change AI Voice

- Open ai_voicetalk_local.py. 
- Find this line: coqui_engine = CoquiEngine(cloning_reference_wav="female.wav", language="en")
- Change "female.wav" to the filename of a wave file (44100 or 22050 Hz mono 16-bit) containing the voice to clone

### Speech end detection

If the first sentence is transcribed before you get to the second one, raise post_speech_silence_duration on AudioToTextRecorder:
    ```
    AudioToTextRecorder(model="tiny.en", language="en", spinner=False, post_speech_silence_duration = 1.5) 
    ```
    
## Contributing

Contributions to enhance or improve the project are warmly welcomed. Feel free to open a pull request with your proposed changes or fixes.

## License

The project is under [Coqui Public Model License 1.0.0](https://coqui.ai/cpml).

This license allows only non-commercial use of a machine learning model and its outputs.

