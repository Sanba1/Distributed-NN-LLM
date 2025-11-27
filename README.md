# Distributed Neural Network for On-Device LLM Inference  
*A mobile-first distributed AI system built using MediaPipe and quantized LLM models.*

## 📖 Overview
This project demonstrates a distributed neural network architecture where multiple mobile devices collaboratively perform LLM inference. Each phone runs a small, quantized language model locally using **Google MediaPipe**, processes a subset of the data, and sends partial results back to a central server for merging.

The system reduces response time and server load by using **data-parallel inference** across devices.

This work was developed as part of my Bachelor's thesis.

---

## 🚀 Features
- Runs a **quantized LLM model locally** on Android using MediaPipe
- Distributed processing across multiple phones
- Local vector search over document chunks
- Lightweight JSON-based communication
- Central summarizer merges partial results into a final answer
- Works fully offline except for sending/receiving messages
- Low memory footprint (mobile-friendly architecture)

---

## 📂 Project Structure
app/
└── src/
└── main/
├── java/
│   └── com/google/mediapipe/examples/llminference/
│        ├── MainActivity.kt
│        ├── InferenceModel.kt
│        ├── ChunkRepository.kt
│        ├── QueryData.kt
│        ├── FirebaseListener.kt
│        ├── LoadJsonFile.kt
│        ├── ChatScreen.kt
│        ├── ChatViewModel.kt
│        ├── QueryListenerService.kt
│        ├── SelectionScreen.kt
│        ├── LoginActivity.kt
│        ├── (and other UI + logic files)
│
├── assets/
│   ├──llm/ # Place only quantized int4.bin model 
│   │    └── model.task
│   ├── json/ # Place PDF chunks with embeddings
│   │    ├── chunk_1.json
│   │    ├── chunk_2.json
│   │    └── ...
│   └── config/               # Optional configs
│
├── AndroidManifest.xml
└── res/

### 📌 Key Components

**`assets/llm/`**  
Contains the quantized MediaPipe LLM model (`model.task`).  
This is the only model required for on-device inference.

**`assets/json/`**  
Contains the preprocessed PDF chunks with embeddings.  
Each device performs local vector search over these files.

**`java/.../llminference/`**  
This is where the main logic lives:
- loading the LLM model  
- running inference  
- reading JSON chunks  
- computing cosine similarity  
- sending partial results to the server (Firestore)  

**`res/layout/`**  
UI layout for the Android app.

---
