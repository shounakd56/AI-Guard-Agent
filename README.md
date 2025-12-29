# AI Guard Agent
## Multimodal Vision–Language Surveillance System


## Overview

AI Guard Agent is a real-time multimodal surveillance system designed to function as an autonomous virtual room guard. The system integrates computer vision, speech processing, and large language model (LLM) reasoning to monitor a physical space, identify trusted individuals, and interact with unrecognized individuals through a structured, escalating security dialogue.

The agent is activated via a spoken command, transitions into continuous monitoring mode, performs face-based authentication using enrolled images, and escalates interaction when an unknown individual is detected. All system responses are delivered both verbally and via terminal output to ensure reliability.

---

## System Architecture

The system follows a fixed three-phase pipeline.

### Phase 1: Listening Mode
- Continuously listens for the activation phrase “guard my room”
- Uses automatic speech recognition to convert microphone input to text
- Activates guard mode upon detecting the phrase

### Phase 2: Guard Mode (Active Monitoring)
- Captures live video feed from the webcam
- Detects faces and generates 128-dimensional facial embeddings
- Compares detected faces with a database of trusted face embeddings

If a trusted face is detected, the system terminates guard mode immediately.

### Phase 3: Security Escalation
- Triggered when an unknown face is detected
- Executes a four-level escalation dialogue
- Requests password verification via speech
- Terminates upon successful authentication or after the final escalation

---

## Key Features

- Voice-activated guard mode using low-latency speech recognition
- Real-time face detection and trusted user authentication
- Four-level escalation logic for unknown individuals
- LLM-driven paraphrasing with strict meta-prompting
- Password-based identity verification using speech-to-text
- Robust fallback behavior when LLM responses fail
- Synchronized spoken and textual system responses

---

## Escalation Dialogue Logic

The system follows a structured escalation sequence.

Level 1  
Polite request for password identification.

Level 2  
Firm warning requesting the password and stating that the room is under surveillance.

Level 3  
Final warning stating that a security alert has been triggered and this is the last opportunity.

Level 4  
System termination.

Each escalation message is paraphrased by the LLM while preserving meaning and enforcing a single-line, plain-text output constraint suitable for text-to-speech.

---

## Technologies Used

Computer Vision  
- face_recognition  
- OpenCV  
- 128-dimensional face embeddings  

Speech Processing  
- Whisper for speech-to-text  
- gTTS / Coqui TTS for audio responses  
- sounddevice for microphone input  

Language and Reasoning  
- Google Gemini Flash  
- Meta-prompting with strict output constraints  
- Fallback base prompts for robustness  

Analysis and Evaluation  
- Structural Similarity Index Measure (SSIM)  
- Mean Squared Error (MSE)  
- Embedding visualization and reconstruction  

---

## Experimental Results

### Face Recognition Validation

Trusted and untrusted individuals were evaluated using facial embedding similarity and reconstructed ghost images.

Trusted vs Trusted  
SSIM: 0.9765  
MSE: 0.0013  

Trusted vs Untrusted  
SSIM: 0.8773  
MSE: 0.0116  

Trusted vs Untrusted  
SSIM: 0.8593  
MSE: 0.0110  

High SSIM and low MSE between trusted images confirm strong intra-subject consistency, while significantly lower SSIM and higher MSE values for untrusted comparisons demonstrate reliable inter-subject separation.

---

## Performance Metrics

- Speech-to-text latency approximately 0.8 seconds
- Real-time face recognition at webcam frame rate
- Stable escalation behavior with and without LLM availability

---

## How to Run

### Prerequisites

pip install whisper face_recognition opencv-python sounddevice torch speechbrain gtts playsound3

### Setup

1. Add images of trusted individuals to the directory:

trusted_faces/

2. Set your Gemini API key inside the code:

API_KEY = "YOUR_GEMINI_API_KEY"

### Execution

Speak “guard my room” to activate monitoring.

---

### Demo Videos & Report

For full system design, architecture diagrams, prompt engineering details, and experimental analysis, refer to the attached course report. 

The demo video files, report as well as the .ipynb file are also available in the folder at link: https://drive.google.com/drive/folders/1MHId4pu_w-8rv-kH3ZC9el-CNP6221AT?usp=drive_link

---

