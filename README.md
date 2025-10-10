## DIO PROJECT - Development of a Multi-Person Facial Recognition System

### Overview

This project implements a **robust facial recognition system** developed for educational purposes. It is built upon state-of-the-art **deep learning** models for detection and facial **embedding** extraction, combined with a classical **machine learning** classifier for identification.

The goal is to accurately identify known (registered) individuals within a dataset, whether in images or video streams. The system is designed to be highly reliable, making it ideal for institutional or school projects.

---

### How It Works

The recognition process is split into two main phases: **Training (Registration/Enrollment)** and **Recognition (Prediction)**.

#### 1. Training Phase:
1.  **Facial Detection (MTCNN):** The system processes the image dataset, using the **MTCNN** (*Multi-task Cascaded Convolutional Networks*) model to precisely locate and crop the faces in each image.
2.  **Embedding Extraction (FaceNet):** The cropped faces are fed into the **FaceNet** model, which converts each face into a 128-dimensional vector (the "facial embedding"). This vector mathematically represents the unique features of the individual's face.
3.  **Classification (SVM):** These **embeddings**, along with the person's name (the *label*), are used to train a **Support Vector Machine (SVM)** classifier. The SVM learns the separation boundaries between the different person classes in the embedding space.
4.  **Model Saving:** The trained SVM model and the **Label Encoder** (used to map names to numerical IDs) are saved using `pickle` for later use.

#### 2. Recognition Phase:
1.  The system reads a new image or video frame.
2.  **Facial Detection and Embedding:** It repeats the detection (MTCNN) and embedding extraction (FaceNet) steps on the unknown face.
3.  **Prediction:** The new facial embedding is fed into the saved **SVM model** to predict the identity.
4.  **Confidence Check:** The prediction is accompanied by a confidence score. If the confidence exceeds a defined **threshold** (e.g., 60%), the person is identified; otherwise, they are labeled as "**Unknown**".
5.  **Result:** The result (name and confidence) is drawn onto the image or video frame.

---

### Technologies and Libraries

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Deep Learning** | **FaceNet** (via `keras-facenet`) | Extracts the unique 128-dimensional facial **embeddings**. |
| **Facial Detection** | **MTCNN** (*Multi-task CNN*) | Robustly detects and localizes faces in images and video frames. |
| **Machine Learning** | **Support Vector Machine (SVM)** | The core classifier used to distinguish between different identities based on the embeddings. |
| **Image Processing** | **OpenCV (`cv2`)** | Handles loading, resizing, BGR/RGB conversion, and drawing bounding boxes/text. |
| **Essentials** | **NumPy, Scikit-learn, Pickle** | Used for array manipulation, label encoding, and saving/loading models. |
