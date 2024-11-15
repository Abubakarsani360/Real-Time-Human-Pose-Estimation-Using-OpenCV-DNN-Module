
# Real-Time Human Pose Estimation Using OpenCV DNN Module

This repository demonstrates real-time human pose estimation using OpenCV's Deep Neural Network (DNN) module with a TensorFlow model (`graph_opt.pb`). The implementation visualizes human skeletons by detecting keypoints (body parts) and connecting them using predefined pose pairs.

---

## 📋 Overview

Pose estimation is a computer vision technique that identifies the configuration of human body parts in an image or video. This project uses OpenCV's DNN module to perform pose estimation in real time, leveraging the pre-trained TensorFlow model.

Key features of this implementation:
- Real-time inference on live camera feeds, videos, or images.
- Visualization of detected body parts and connections as a skeleton.
- Configurable confidence thresholds for accurate detection.
- Demonstrates the capabilities of OpenCV's DNN module for TensorFlow-based models.

---

## 🧠 Model Details

The implementation uses a **TensorFlow pre-trained model** converted to a `.pb` format, compatible with OpenCV's DNN backend. 

### Model Highlights:
- **Model File**: `graph_opt.pb`
- **Framework**: TensorFlow
- **Architecture**: OpenPose-like model with a reduced number of output layers optimized for lightweight deployment.
- **Output Format**:
  - A 4D blob: `[1, 57, H, W]` (where `H` and `W` are the spatial dimensions).
  - The first 19 channels correspond to key body parts' heatmaps.

### Body Parts Detected:
| Index | Body Part       | Index | Body Part    |
|-------|-----------------|-------|--------------|
| 0     | Nose            | 10    | RAnkle       |
| 1     | Neck            | 11    | LHip         |
| 2     | RShoulder       | 12    | LKnee        |
| 3     | RElbow          | 13    | LAnkle       |
| 4     | RWrist          | 14    | REye         |
| 5     | LShoulder       | 15    | LEye         |
| 6     | LElbow          | 16    | REar         |
| 7     | LWrist          | 17    | LEar         |
| 8     | RHip            | 18    | Background   |
| 9     | RKnee           |       |              |

---

## 🔧 Technical Implementation

### Dependencies

- **Python 3.8 or later**
- **OpenCV with DNN support**:
  ```bash
  pip install opencv-python opencv-python-headless
  ```

### Core Steps

1. **Load Pre-trained Model**:
   The TensorFlow model is loaded using `cv.dnn.readNetFromTensorflow()`, which reads `.pb` files directly.

2. **Frame Preprocessing**:
   - Input frames are resized to specified dimensions (`--width`, `--height`).
   - Normalization is applied: `(127.5, 127.5, 127.5)` subtraction for color scaling.

3. **Model Inference**:
   - The output blob from the model represents confidence heatmaps for body part positions.
   - Thresholding is applied (`--thr`) to filter out low-confidence detections.

4. **Pose Visualization**:
   - Identified points are connected based on predefined `POSE_PAIRS`.
   - Each body part is represented as a point (`cv.ellipse`), and connections are drawn using `cv.line`.

---

## 🚀 Getting Started

### Prerequisites
1. Download the pre-trained model (`graph_opt.pb`).
2. Ensure your environment has OpenCV with DNN support installed.

### Running the Script

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/human-pose-estimation.git
   cd human-pose-estimation
   ```

2. Run the script:
   - To process a video:
     ```bash
     python pose_estimation.py --input path_to_video.mp4
     ```
   - To use the webcam:
     ```bash
     python pose_estimation.py
     ```

3. Custom configurations:
   - Specify input dimensions:
     ```bash
     python pose_estimation.py --width 432 --height 368
     ```
   - Set detection confidence threshold:
     ```bash
     python pose_estimation.py --thr 0.3
     ```

---

## 📂 File Structure

- **pose_estimation.py**: Main script for real-time pose estimation.
- **graph_opt.pb**: TensorFlow model used for pose detection.
- **README.md**: Documentation for the repository.

---

## ⚙️ Performance Metrics

- **Inference Time**: Displayed on the output video in milliseconds (`t`).
- **Model Accuracy**: Determined by the confidence threshold (`--thr`).

Performance may vary based on:
- Input dimensions (`--width`, `--height`).
- Hardware capabilities (CPU/GPU support in OpenCV DNN).

---

## 🛠️ Future Work

1. **Extend Support for Multi-Person Detection**:
   - Current implementation is optimized for single-person pose estimation.
   - Multi-person support can be added using OpenPose-like extensions.

2. **Enhance Real-Time Performance**:
   - Leverage GPU acceleration for faster inference.
   - Optimize the model for mobile or embedded devices.

3. **Integrate Additional Features**:
   - Support for custom datasets for specialized pose estimation tasks.

---

## 📜 License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

Feel free to explore and enhance the repository! For any issues or contributions, open a GitHub issue or submit a pull request.
