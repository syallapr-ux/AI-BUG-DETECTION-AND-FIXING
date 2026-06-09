# AI-BUG-DETECTION-AND-FIXING
# AI Python Bug Fixer ⚡

An interactive, real-time web application that automatically identifies and repairs syntactical and logical bugs in Python code. This project bridges a modern, responsive web frontend with a high-performance deep learning backend: a custom fine-tuned Qwen-2.5-Coder-7B model optimized with Unsloth 4-bit quantization, running on a hosted Google Colab T4 GPU, and securely bridged via Flask and Ngrok.

## 🚀 Repository Structure

* **index.html**: The interactive client-side dashboard featuring a responsive dual-pane code editor (dark mode) and unified REST handshakes.
* **Notebooks**: Contains the complete pipeline for setting up, training/fine-tuning the Qwen model on the CodeAlpaca-20k dataset, running the inference engine, and hosting the live background API server.

---

## 🏗️ Technical Architecture

The system functions through a secure pipeline:

1. **Interactive Web UI**: A browser-based interface sends code via a secure POST payload with CORS & Skip-Warning headers.
2. **Ngrok Tunnel**: Establishes a secure port-forwarding tunnel from the local Colab environment to the internet.
3. **Flask API**: An API running on the Colab environment acts as the bridge.
4. **Inference Engine**: The request is processed by the Qwen-2.5-Coder-7B (Fine-tuned + 4-bit Quantized) model using high-speed GPU inference.
5. **Response**: The parsed and cleaned code is returned back to the UI.

---

## 🛠️ Key Technologies

* **Model Accelerator**: Unsloth AI — provides 2x faster training and ultra-low VRAM inference.
* **Base Language Model**: Qwen2.5-Coder-7B-Instruct (quantized to 4-bit).
* **Dataset**: Fine-tuned on the `sahil2801/CodeAlpaca-20k` code-repair distribution.
* **Web Framework**: Flask with robust Cross-Origin Resource Sharing (Flask-CORS).
* **Secure Tunneling**: Ngrok API with customized HTTP headers.

---

## 📖 Setup & Playbook

### Step 1: Initialize the GPU Backend
1. Open your notebook in Google Colab and set your Runtime type to **T4 GPU**.
2. Run the cells to install dependencies (`Unsloth`, `xformers`, `PyTorch`, etc.).
3. Restart your session to apply CUDA library bindings.
4. Initiate the Flask server daemon.
5. Provide your personal Ngrok Auth token inside the Ngrok setup cell, and execute it to generate your stable API gateway URL: `https://<your-subdomain>.ngrok-free.app`

### Step 2: Configure the Client Page
1. Open `index.html` in an editor.
2. Update the API connection string in the JavaScript fetch block with your newly generated stable endpoint.
3. Open `index.html` locally in any modern browser, or host it instantly using GitHub Pages.

### Step 3: Clear the Tunnel Security
Because Ngrok free accounts show an interstitial warning page to fresh visitors, the system uses a custom `ngrok-skip-browser-warning: true` header. To guarantee a smooth handshake on first run:
1. Paste your root Ngrok URL directly into a browser tab and click **"Visit Site"** if prompted.
2. Once you see `{"status":"ok"}` on the screen, your browser is registered, and the web interface is ready.

---

## 📝 Performance Benchmarks

* **Average Fix Latency**: ~1.2 to 2.5 seconds.
* **GPU Memory Consumption**: Fits comfortably under 7.5 GB of active VRAM during inference, ensuring stable performance on standard free-tier T4 cloud runtimes.
