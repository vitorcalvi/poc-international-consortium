# Privacy Policy for POC-International-Consortium

**Effective Date:** September 16, 2026  
**Last Updated:** September 16, 2026  
**Application ID:** `com.dyagnosys.pocmentalhealth`  
**Developer Contact:** `vcalvi@gmail.com`  
**Institutional Partner:** Universidade Federal de Minas Gerais (UFMG)  

---

## 1. Introduction & Overview

Welcome to **POC-International-Consortium** ("the Application"), developed by the POC-International-Consortium research initiative in partnership with the **Universidade Federal de Minas Gerais (UFMG)**. 

POC-International-Consortium is an investigational research application designed to evaluate on-device multimodal machine learning algorithms for mental health and depression screening. The application analyzes facial expressions and acoustic voice patterns to calculate exploratory screening indicators aligned with standardized psychological instruments (such as the PHQ-9).

We are committed to the highest standards of data privacy and medical ethics. This Privacy Policy explains our strict **offline-first, zero-cloud architecture**, detailing how device permissions are utilized, how data is processed locally, and why no personal, biometric, or health data ever leaves your smartphone.

---

## 2. Core Privacy Principle: 100% On-Device Processing

The architectural foundation of POC-International-Consortium is **Privacy-by-Design**:

- **Zero Cloud Data Transmission:** The Application does **not** transmit, upload, backup, or stream any raw audio, raw video, still photographs, facial landmark coordinates, voice features, or biometric embeddings to remote servers, cloud backends, or third parties.
- **Zero Third-Party Trackers or Analytics SDKs:** The Application contains **no** advertising networks, no commercial trackers, and no external analytics software (e.g., zero Google Analytics, Firebase Analytics, Meta SDK, or Mixpanel).
- **Fully Offline Functional:** All neural network inferences execute entirely within the local execution environment of your device using embedded ONNX Runtime Mobile (`onnxruntime-react-native`). The Application does not require an active internet connection to evaluate screening tasks.

---

## 3. Permissions & Device Capabilities Utilized

To execute screening assessments, POC-International-Consortium requests access to specific device hardware:

### 3.1 Camera (`android.permission.CAMERA` / iOS `NSCameraUsageDescription`)
- **Purpose:** Enables real-time facial expression recognition (FER), facial landmark localization, and anti-spoofing liveness verification.
- **How It Operates:** Video frames captured by the camera are streamed directly to device RAM, processed frame-by-frame by lightweight on-device neural networks (YuNet, MobileFaceNet, MiniFASNet-V2, EmoNext-tiny, and ViT-Distil), and immediately overwritten in volatile memory.
- **Storage & Transmission:** **Zero images or video files are saved to permanent device storage or uploaded to the internet.**

### 3.2 Microphone (`android.permission.RECORD_AUDIO` / iOS `NSMicrophoneUsageDescription`)
- **Purpose:** Extracts digital acoustic biomarkers (fundamental frequency $F_0$, jitter, shimmer, mel-frequency cepstral coefficients [MFCCs], and prosodic duration) during guided phonation tasks for depression screening.
- **How It Operates:** Audio recordings captured during phonation tasks are processed locally in device RAM using digital signal processing (DSP) and an on-device recurrent neural network (BRIDGE-2-AI bi-LSTM).
- **Storage & Transmission:** Raw audio is **never** uploaded to any external server. Temporary cache files created during audio format conversion (e.g., AMR-NB to WAV) reside strictly in the application-sandboxed local cache directory and are deleted automatically or whenever the user clears the cache.

---

## 4. On-Device Machine Learning Models & Biometrics

All artificial intelligence and machine learning pipelines embedded in POC-International-Consortium execute via **ONNX Runtime**:

| Task | Neural Network Architectures | Execution Location | Data Persisted |
| :--- | :--- | :--- | :--- |
| **Face Detection & Alignment** | YuNet, MobileFaceNet | Local device CPU/NPU | None (ephemeral in RAM) |
| **Liveness Verification** | MiniFASNet-V2 | Local device CPU/NPU | None (ephemeral in RAM) |
| **Facial Expression (FER)** | EmoNext-tiny (int8), ViT-Distil (int8) | Local device CPU/NPU | Categorical score only (local) |
| **Acoustic Biomarkers** | BRIDGE-2-AI bi-LSTM (FP16) | Local device CPU/NPU | Screening score only (local) |

**Biometric Template Protection:** POC-International-Consortium does not construct a permanent biometric facial identification template or voiceprint capable of identifying you across systems. Any localized session representations (such as intermediate feature vectors) exist only in memory during the active session. If local enrollment is utilized, embeddings are encrypted using AES-256 encryption within the OS-sandboxed secure storage (MMKV / EncryptedStorage) and never exported.

---

## 5. Local Data Storage, Security & Retention

- **Local-Only Storage:** Any screening scores, session timestamps, or questionnaire responses are persisted solely within the application's private sandbox directory on your device.
- **Encryption:** Stored data is protected by hardware-backed sandbox encryption provided by Android/iOS operating system security layers and AES-256 encrypted storage.
- **Retention & Deletion:** 
  - All local session logs are maintained only as long as you keep the Application installed or until you explicitly delete session history within the Application settings.
  - Uninstalling the Application permanently and irreversibly deletes all local sandboxed data, caches, and encryption keys from your device.

---

## 6. Academic Research Partnership with UFMG

POC-International-Consortium was created as part of an academic research initiative in collaboration with researchers at the **Universidade Federal de Minas Gerais (UFMG)**. The application serves as an experimental validation platform to assess whether on-device machine learning can deliver accurate, low-latency, and privacy-preserving behavioral screening without compromising user confidentiality or transferring sensitive health data to third-party institutions.

---

## 7. Medical & Clinical Disclaimer

> **IMPORTANT NOTICE:**  
> **POC-International-Consortium is an investigational research and preliminary screening application. It is NOT a certified medical device and is NOT intended for clinical diagnosis, treatment, cure, mitigation, or prevention of any medical or psychological condition, including clinical depression, anxiety disorders, or suicide risk.**
>
> - The screening results generated by POC-International-Consortium are preliminary indicators intended solely for research, educational, and personal self-awareness purposes.
> - POC-International-Consortium does **not** replace the clinical judgment, evaluation, or diagnosis of a licensed physician, psychiatrist, psychologist, or healthcare provider.
> - Never disregard professional medical advice or delay seeking professional medical evaluation because of information or screening results obtained through this application.
>
> **Crisis Support Resources:**  
> If you are experiencing distress, severe mental anguish, or thoughts of self-harm, please reach out to emergency services or a national crisis helpline immediately:
> - **Brazil:** Centro de Valorização da Vida (CVV) — Call **188** (toll-free, 24/7) or visit [cvv.org.br](https://www.cvv.org.br).
> - **United States:** Suicide & Crisis Lifeline — Call or text **988** (available 24/7) or visit [988lifeline.org](https://988lifeline.org).
> - **International:** Consult [findahelpline.com](https://findahelpline.com) or contact your local emergency hospital.

---

## 8. Compliance with International Privacy Regulations

Because POC-International-Consortium does not collect, transmit, or process personal data on external servers, our architecture satisfies the highest standards of international data privacy frameworks:

### 8.1 General Data Protection Regulation (GDPR — EU/UK)
- **Legal Basis:** Processing of on-device sensor data occurs strictly pursuant to user consent when granting camera and microphone runtime permissions.
- **Data Minimization:** No personal data is collected or transferred to any data controller or processor.
- **Data Subject Rights:** Because no data is stored on remote servers, rights of access, rectification, portability, and erasure are exercised directly by the user on the device (by clearing app storage or uninstalling the app).

### 8.2 Lei Geral de Proteção de Dados (LGPD — Brazil)
- Em total conformidade com a Lei nº 13.709/2018 (LGPD), o POC-International-Consortium não realiza coleta, compartilhamento ou transferência de dados pessoais ou dados pessoais sensíveis (biometria ou saúde) para servidores externos. O processamento é 100% local no dispositivo do usuário.

### 8.3 California Consumer Privacy Act (CCPA / CPRA)
- POC-International-Consortium does not sell, share, or disclose personal information to any third party for commercial or any other purposes.

---

## 9. Children's Privacy

POC-International-Consortium is intended exclusively for adult research participants and general users aged **18 and older**. We do not knowingly collect, process, or solicit information from children under 13 (or under 18). If we become aware that a child under 13 has provided sensor data, our 100% ephemeral processing ensures no such data is stored remotely.

---

## 10. Changes to this Privacy Policy

We may update this Privacy Policy from time to time to reflect modifications in software architecture, legal obligations, or research protocols. Any updates will be published within the application repository and updated in future application releases with a revised "Last Updated" date.

---

## 11. Contact Information

If you have questions, feedback, or concerns regarding this Privacy Policy or the data protection practices of POC-International-Consortium, please contact the development team:

- **Email:** `vcalvi@gmail.com`
- **Institutional Affiliate:** Universidade Federal de Minas Gerais (UFMG)
