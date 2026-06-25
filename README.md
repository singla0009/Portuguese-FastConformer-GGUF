# Portuguese FastConformer-Hybrid GGUF (Portuguese ASR)

Welcome to the GitHub homepage for the highly optimized **GGUF** (float32) conversion of the `nvidia/stt_pt_fastconformer_hybrid_large_pc` model. This is a FastConformer Automatic Speech Recognition (ASR) model specifically trained for **Portuguese (pt)** speech-to-text, featuring native support for punctuation and capitalization (P&C).

**[Download the Model from Hugging Face Here](https://huggingface.co/Singla0009/Portuguese-FastConformer-GGUF)**

---

### 💻 Integrates perfectly with CAPIT
This model was explicitly converted and optimized to be run inside **CAPIT**—our custom desktop transcription software. 

**What is CAPIT?**
CAPIT is a fully offline, high-speed transcription application. It is built using Rust and Tauri, meaning it is incredibly lightweight, fast, and 100% private (no audio is ever sent to the cloud). Instead of writing python code or using terminal commands, you can simply load this model into the CAPIT desktop app and transcribe audio instantly with a beautiful user interface.

**[Check out the CAPIT Desktop App Here!](https://github.com/singla0009)**

---

The model is designed for high-performance, local deployment with zero Python dependencies using the lightweight C++ `parakeet-cpp` engine (GGML backend). 

> [!IMPORTANT]
> The GGUF file is fully standalone. Configuration parameters and the 128-token sentencepiece vocabulary are embedded directly inside the binary.

## Model Details
*   **Architecture:** FastConformer Hybrid CTC/RNN-T (Large)
*   **Parameter Count:** ~115M
*   **Vocabulary Size:** 128 tokens
*   **Punctuation & Capitalization:** Yes, natively supported (emits upper/lower case text, spaces, periods, commas, and question marks).
*   **Training Data:** ~2,200 hours of Portuguese speech (Common Voice, Multilingual LibriSpeech, and a large proprietary corpus).
*   **Input Format:** 16,000 Hz mono-channel WAV audio.

---

## Evaluation & Analytics

### 1. Accuracy Benchmarks (WER & CER)

| Dataset / Test Set | Decoder Head | Word Error Rate (WER) | Character Error Rate (CER) |
| :--- | :--- | :--- | :--- |
| **Common Voice 16.0** | RNNT | **12.03%** | **3.20%** |
| **Common Voice 16.0** | CTC | **12.83%** | **3.39%** |
| **Multilingual LibriSpeech** | RNNT | **24.78%** | **5.92%** |
| **Multilingual LibriSpeech** | CTC | **25.70%** | **6.18%** |

### 2. Local Performance & Speed Benchmarks
Tested on local hardware:
*   **Test Audio Duration:** 7.26 seconds (mono, 16000Hz).
*   **Metric:** Real-Time Factor (RTF). Lower is faster.

| Configuration | Average Inference Time | Real-Time Factor (RTF) | CPU / RAM Footprint |
| :--- | :--- | :--- | :--- |
| **Portuguese Hybrid (GPU / CUDA)** | **0.490s** | **0.067x (14.9x speed)** | ~520 MB VRAM |
| **Portuguese Hybrid (CPU)** | **0.395s** | **0.054x (18.5x speed)** | ~140 MB RAM |

---

## Usage Instructions

To run this model, you need the **parakeet-cli** C++ execution engine.

1. Go to the [parakeet.cpp GitHub Repository](https://github.com/PABannier/parakeet.cpp).
2. Follow their build instructions to compile the `parakeet-cli` executable for your specific operating system (Windows/Linux/macOS).
3. Once compiled, open your terminal and run the model using the following command:

```bash
parakeet-cli transcribe --model portuguese-fastconformer-hybrid-large.f32.gguf --input audio.wav --decoder ctc --lang pt
```

## Credits and Licenses
*   **Original Checkpoint:** [nvidia/stt_pt_fastconformer_hybrid_large_pc](https://huggingface.co/nvidia/stt_pt_fastconformer_hybrid_large_pc)
*   **License:** Under NVIDIA NGC Terms of Use / CC-BY-4.0.
