# **Qompute-AI: Zero Loss Protocol**  // **Frontier AI Support Kit & Lossless Quantization Suite**

Official release documentation for the **QomputeAI Frontier AI Support Kit**. This repository houses the runtime tools, compiler artifacts, and **95 Apple-notarized, code-signed static binaries** compiled for high-performance quantum-affect virtualized workloads. It provides full native support for the **QFX Series** lossless quantization engine and **QSD** compiled model runtimes.

## **⚡ Installation**

The suite is distributed as a macOS Signed & Notarized Installer (.pkg), deploying all static binary images directly to /usr/local/bin.

### **Option A: GUI Installation**

1. Download QomputeAI-Frontier-AI-Support-Kit.pkg.  
2. Double-click to open and follow the macOS Installer prompts.

### **Option B: Terminal / Silent Installation**

sudo installer \-pkg "/path/to/releases/QomputeAI-Frontier-AI-Support-Kit.pkg" \-target /

## **🚀 QFX32 Execution Modes & Loader Configuration**

The **QFX32** loader supports dynamic memory-vs-throughput trade-offs controlled by the GGML\_QFX32\_DEQUANT environment variable.

// QFX32: Optional dequant-on-load (opt-in via GGML\_QFX32\_DEQUANT=1).  
// Default: streaming mode (2.3 GB RAM, lower throughput).  
// With env var: decode to f32 at load time (4.6 GB RAM, native f32 speed).  
if (cur-\>type \== GGML\_TYPE\_QFX32 && getenv("GGML\_QFX32\_DEQUANT")) { ... }

| Execution Mode | Env Variable | Memory Footprint | Performance & Behavior |
| :---- | :---- | :---- | :---- |
| **Streaming Mode** *(Default)* | *(Unset)* | **\~2.3 GB RAM** | Low memory footprint; streams dequantization dynamically during inference. |
| **Native Speed Mode** | GGML\_QFX32\_DEQUANT=1 | **\~4.6 GB RAM** | Decodes tensors to native f32 at load time for maximum throughput (**17.8 t/s**). |

### **Quickstart Example**

\# 1\. Run in Default Low-Memory Streaming Mode (\~2.3 GB RAM)  
llama-server \-m models/qfx32-model.gguf

\# 2\. Run in High-Performance Pre-Decoded f32 Mode (\~4.6 GB RAM)  
export GGML\_QFX32\_DEQUANT=1  
llama-server \-m models/qfx32-model.gguf

## **📦 Binary Artifacts (95 Total)**

The package deploys **95 static binary images** to /usr/local/bin. Key executables include:

### **Core Runtimes & Engine**

* llama-server — Production REST/HTTP inference server.  
* llama-cli / llama — Interactive CLI chat and inference driver.  
* llama-quantize — Model quantization tool supporting QFX/QSD matrix formats.  
* llama-bench / llama-batched-bench — Latency and throughput benchmark suite.

### **Specialized & Multimodal Drivers**

* llama-gemma3-cli / llama-qwen2vl-cli / llama-minicpmv-cli — Multimodal VLM drivers.  
* llama-diffusion-cli / llama-diffusion-gemma-server — Image generation and diffusion servers.  
* llama-embedding / llama-retrieval / llama-cvector-generator — Vector embeddings and representation tooling.  
* llama-finetune / llama-export-lora / llama-imatrix — Fine-tuning, LoRA extraction, and importance matrix generators.

### **Utilities & Verification**

* llama-gguf-split / llama-gguf-hash — GGUF file operations and integrity validation.  
* export-graph-ops — Computation graph export and inspection tool.  
* Full test suite binaries (test-backend-ops, test-quantize-perf, test-thread-safety, test-rope, etc.).

## **🔒 Code Signing, Notarization & Gatekeeper Status**

All 95 binaries and the host installer package are signed using official Developer ID credentials, notarized by Apple Notary Services, and ticket-stapled for offline validation.

* **Developer Identity:** Developer ID Installer: qomputeai inc (4HMYMNKRGB)  
* **Gatekeeper Assessment:** Accepted (source=Notarized Developer ID)

### **Verify Package Integrity**

spctl \--assess \--type install \-v /path/to/QomputeAI-Frontier-AI-Support-Kit.pkg  
