## Demonstration Video

【Real-Time Visual Instruction and Feedback System for Effective CPR Training】
[![CPR Training Demo](https://img.shields.io/badge/Demo-Video-blue)](https://www.bilibili.com/video/BV1DwPoekEL3)

## **Abstract**

CPR is crucial for reviving patients during the initial minutes of sudden cardiac arrest. Public proficiency is required in these life-saving techniques. However, traditional first-aid training processes to improve proficiency consume high human resource and material costs. The traditional training methods face several challenges, including high costs associated with specialized equipment and the lack of personalized feedback and precise guidance. These limitations hinder scalability and accessibility, making it difficult to train large populations effectively. In response, we first conduct detailed investigations with experts to identify the requirements for an improved training system. Then we propose RescueRadar, an interactive real-time visualization solution specifically designed for CPR training. RescueRadar addresses the limitations of traditional methods through a combination of static and dynamic indicators. The realization of these design objectives is facilitated by the strategic integration of visual cues, pivotal data charts, and elucidative guidance text. Supported by user studies and experts, our investigations demonstrate the effectiveness, professionalism, and accuracy of the solution. RescueRadar significantly improves users' understanding and mastery of CPR techniques.

## **System Interface**
![RescueRadar](https://github.com/user-attachments/assets/55377079-45ef-4da0-9070-ecf6443b8902)

- (A) The control panel, including functions such as switching real-time cameras or video files as input, starting and ending recording, etc.; 
- (B) The output image after overlaying four types of visual clues; 
- (C) Extracted interactive 3D bone maps; 
- (D) The evaluation panel, where the (D2) area continuously updates specific error information over a period of time, and the (D1) extracted visual guidance text; 
- (E) Current display angle (E1) and historical distribution scatter (E2) chart; 
- (F) Current press status (F1) and historical distribution curve (F2) chart;
- (G) The "Consistency of Press" parallel coordinate system reflects the coordination changes of posture during CPR process; 
- (H) Current frequency chart; 
- (I) The "Comprehensive Performance" score stack chart reflects the weighted total performance of each indicator.

## User Instruction
Open the **"Source Code"** folder, click on **"index.html"** to enter the system interface. 
After entering the interface, you can select video input or file input in the left control panel. Video input can automatically start training, while file input requires clicking the blue play button below the video box to start training.

The recommended display resolution for this project's webpage is **2560x1440**; If the display resolution is 1920x1080, please zoom the browser to 75% and click the 'Refresh' button to make the page layout responsive and restore normal style.

## Dependencies
**For model training & testing only** (not required for runtime):
```python
Python 3
torch==2.1.0
pandas==1.5.3
numpy==1.23.5
scikit-learn==1.2.1
matplotlib==3.7.1
tqdm==4.65.0
```

## Source Code Structure
| File | Description |
|------|-------------|
| `angleCount.js` | Real-time joint angle monitoring and performance recording |
| `angleRangeControl.js` | Posture angle constraint management |
| `chart.js` | CPR metrics visualization (depth, frequency, etc.) |
| `collideForce.js` | Compression force estimation and feedback |
| `control.js` | Core system operations and UI management |
| `finalReport.js` | Comprehensive evaluation report generation |
| `frequency.js` | Real-time compression frequency calculation |
| `heatmap.js` | Training performance heatmap visualization |
| `inputImage.js` | Video stream processing module |
| `landmarkAngle.js` | Key body angles analysis (Angle1-Angle3) |
| `landmarkTrack.js` | Body landmark trajectory tracking |
| `model.js` | Posture recognition model integration |
| `outputImage.js` | Visual feedback rendering |
| `outputVideoControl.js` | Training video management |
| `parallel.js` | Joint coordination visualization |
| `pose.js` | Real-time posture quantification |
| `scoreboard.js` | Performance scoring display |
| `skeleton.js` | Body skeleton visualization |
| `teachCPR.js` | Core training logic with multimodal feedback |

## Core Algorithms

### CPR Frequency Gaussian Smoothing
**I. Adaptive Gaussian Kernel Construction**  
- Sigma selection based on human compression dynamics  
- 3× fluctuation period coverage with odd-length symmetry  
- Time-decaying weight distribution for jitter suppression  
- Normalized historical/future frame influence  

**II. Temporal Denoising Process**  
- Context-aware sliding window (50-120bpm range)  
- Boundary-preserving waveform processing  
- Weighted time-domain fusion with error compensation  

**III. Medical Signal Optimization**  
- Dynamic edge normalization strategy  
- Jitter removal with waveform integrity preservation  
- Peak detection error reduction < 1.2%  

### Posture Guidance Autoencoder
**I. Model Architecture**  
```mermaid
graph LR
A[17D Mediapipe Input] --> B(Encoder)
B --> C[256D Latent Space]
C --> D(Decoder)
D --> E[17D Reconstruction]
```

**II. Training Process**  
- Adam optimizer (lr=0.01) with MSE reconstruction loss  
- 100-epoch training cycle with batch processing  
- Threshold: μ + 2σ reconstruction error  

**III. Detection Workflow**  
1. Real-time keypoint encoding  
2. Reconstruction error calculation  
3. Visual deviation highlighting  
4. Correction vector generation  

## Dataset Specification
**Format**:
- 99 columns: x/y/z coordinates of 33 body landmarks  
- 100th column: CPR phase (0=compression, 1=release)  

**Recommendations**:
- Coordinate normalization (0-1 range)  
- Column 100 exclusion for posture recognition  
- Augmentation for position/orientation variance  

## Experimental Setup
### Experimental Site
![5a1fdf0cc8923a3f4f04088143810b35](https://github.com/user-attachments/assets/02521326-b6a5-425f-9cd3-b9aead80c0cb)

### Environment Configuration
- University yoga classroom (30-person capacity)  
- 45° camera angle with controlled lighting  
- CPR simulation pillow (7cm height)  

### Participant Management
- Batch processing (5 participants/group)  
- 20-40 minute sessions  
- Physical support:  
  - 550ml water + energy snacks  
  - Informed consent + safety protocols  

### Data Collection
- Automatic session recording + evaluation reports  
- Mixed assessment tools:  
  - Objective multiple-choice (0/1 scoring)  
  - 7-point Likert scale feedback  
  - System-generated performance metrics  

## Statistical Analysis
**Data Files**:
- `RescueRadar User Study-1/2/3.pdf`  
- `RescueRadar Expert Interview.pdf`  
- `RescueRadar Data.xlsx` (Raw/Core Data sheets)  

**Methods**:
- T-distribution analysis  
- 95% confidence interval estimation  
- Wilcoxon signed-rank tests  
