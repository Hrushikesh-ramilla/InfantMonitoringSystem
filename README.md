# Infant Monitoring System with Raspberry Pi 5

This project is an **infant monitoring system** designed to run on a **Raspberry Pi 5** using a webcam, microphone, and a temperature sensor. It leverages computer vision, audio processing, and environmental sensing to monitor the baby's safety and comfort in real time.

---

## 🧠 Key Features

- **Real-Time Sleep Detection** using Dlib-based eye aspect ratio (EAR).
- **Cry Detection** using a custom-trained audio classification model (Random Forest).
- **Pose Detection** using MediaPipe to identify risky positions like:
  - Face down
  - Face covered
  - Body uncovered
- **Temperature Awareness** to alert if the baby is uncovered and the surrounding temperature is too low.
- **Crying Response** plays a soothing song if the baby is detected crying.
- **Audio Threading** for non-blocking cry detection.

---

## 🧰 Hardware Used

- Raspberry Pi 5
- Webcam (USB or Pi Camera Module)
- Microphone (USB or 3.5mm mic)
- DHT22 or similar temperature sensor

---

## 🧩 Project Structure

```
baby_cry_detection/
├── pc_methods/
│   ├── record_audio.py
│   ├── train_classifier.py
│   ├── feature_engineer.py
├── rpi_methods/
│   ├── baby_cry_predictor.py
│   ├── feature_engineer.py
│   ├── majority_voter.py
│   ├── reader.py
│   ├── temperature_sensor.py  <- NEW
├── output/
│   ├── model/model.pkl
│   ├── dataset/dataset.npy, labels.npy
├── main_monitoring_script.py
```

---

## 🚀 How It Works

1. **Video Processing:**
   - Uses OpenCV and MediaPipe to detect pose and check facial orientation.
   - Uses Dlib to track eye openness and determine sleep state.

2. **Cry Detection:**
   - When the baby is awake, a 9-second audio is recorded.
   - Feature engineering is applied, followed by classification with the trained model.

3. **Alerts:**
   - If face is down/covered or camera is obstructed, alerts are raised.
   - If the baby is uncovered **and** the room temperature is below a threshold, an alert is triggered.
   - If the baby is crying, a soothing song is played.

---

## 📦 How to Run

1. **Set up hardware:**
   - Connect webcam, mic, and temperature sensor to the Pi.

2. **Install requirements:**
   ```bash
   pip install opencv-python mediapipe dlib pyaudio simpleaudio Adafruit_DHT
   ```

3. **Train model (optional):**
   ```bash
   python train_set_generator.py  # Feature extraction
   python train_model.py          # Model training
   ```

4. **Run monitor:**
   ```bash
   python main_monitoring_script.py
   ```

---

## 🛡 Alerts Raised

- 🚼 Face Down
- 😴 Sleeping
- 😨 Face Covered or Not Detected
- 🧥 Body Uncovered (with temperature check)
- 🔊 Crying
- 📷 Camera Obstructed

---

## 📁 Data Used for Training

Training data consists of labeled 9-second audio clips categorized into different folders (e.g., `0`, `1` where 1 = crying). Feature vectors are extracted and used to train a classifier using `RandomForestClassifier`.

---

## 🎵 Soothing Music
You can replace the `alone_again_01.wav` with your preferred lullaby or calming music.

---

## 👥 Authors
- [Your Name]
- [Collaborator if any]

---

## 📌 To Do
- Add mobile notification support
- Upgrade to TensorFlow Lite for edge-optimized cry detection
- Improve robustness of face detection using MediaPipe Face Mesh

---

## 📜 License
This project is for educational and non-commercial use.

