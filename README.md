# Awake-AI---Drowsiness-Detection-System-

A real-time drowsiness detection system designed for classroom environments using MediaPipe Face Mesh, Eye Aspect Ratio (EAR) calculation, and computer vision techniques.

## 🎯 Features

- **Real-time Face Detection**: Uses MediaPipe Face Mesh to detect 468 facial landmarks
- **Eye Aspect Ratio (EAR) Calculation**: Monitors eye closure patterns
- **Drowsiness Alert System**: Triggers visual and audio alarms when drowsiness is detected
- **Statistics Tracking**: Records blinks, drowsy events, and session duration
- **Low Computational Requirements**: Runs efficiently on standard hardware
- **Multi-student Monitoring**: Can be adapted for multiple students (currently set to 1)

## 📋 System Requirements

- Python 3.8 or higher
- Webcam or camera
- Operating System: Windows, macOS, or Linux
- Minimum 4GB RAM
- Good lighting conditions for optimal performance

## 🚀 Installation

### Step 1: Clone or Download the Repository

```bash
# If using git
git clone <repository-url>
cd drowsiness-detection-system

# Or download and extract the ZIP file
```

### Step 2: Create a Virtual Environment (Recommended)

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

## 📖 Usage

### Running the System

```bash
python drowsiness_detection_system.py
```

### Controls

- **Press 'q'**: Quit the application
- **Press 'ESC'**: Alternative quit method

### Understanding the Display

The system displays:
- **ALERT (Green)**: Student is awake and alert
- **DROWSINESS ALERT! (Red)**: Student is drowsy (eyes closed for extended period)
- **EAR Value**: Current Eye Aspect Ratio (typically 0.2-0.4 when awake)
- **Frames**: Number of consecutive frames with closed eyes
- **Time**: Session duration
- **Blinks**: Total number of blinks detected
- **Drowsy Events**: Number of times drowsiness was detected

## 🔧 How It Works

### 1. Face Detection
The system uses MediaPipe Face Mesh to detect faces and extract 468 facial landmarks in real-time.

### 2. Eye Landmark Extraction
Specific landmarks are extracted for the left and right eyes:
- **Left Eye**: Landmarks [362, 385, 387, 263, 373, 380]
- **Right Eye**: Landmarks [33, 160, 158, 133, 153, 144]

### 3. Eye Aspect Ratio (EAR) Calculation
The EAR formula measures the eye opening:

```
EAR = (||p2-p6|| + ||p3-p5||) / (2 * ||p1-p4||)
```

Where:
- p1-p4: Horizontal eye landmarks
- p2, p3, p5, p6: Vertical eye landmarks

### 4. Drowsiness Detection
- If EAR < 0.25 for 20 consecutive frames, drowsiness is detected
- An alarm is triggered
- Visual warnings are displayed

### 5. Alert System
- **Visual Alert**: Red border around the frame
- **Text Alert**: "DROWSINESS ALERT!" message
- **Audio Alert**: Alarm sound (440 Hz beep)

## ⚙️ Configuration

You can modify the following parameters in the code:

```python
# Eye Aspect Ratio threshold
EAR_THRESHOLD = 0.25  # Lower = more sensitive

# Number of consecutive frames to trigger alert
CONSECUTIVE_FRAMES = 20  # Higher = less sensitive

# Camera resolution
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)
```

## 📊 Technical Details

### MediaPipe Face Mesh
- **468 3D landmarks**: Comprehensive facial mapping
- **Real-time processing**: Optimized for live video streams
- **Multi-face support**: Can detect multiple faces (configurable)

### Eye Aspect Ratio (EAR)
- **Normal range**: 0.25 - 0.4 (eyes open)
- **Closed eyes**: < 0.25
- **Threshold-based detection**: Adjustable sensitivity

### Alarm System
- **Frequency**: 440 Hz (A4 musical note)
- **Duration**: 0.5 seconds
- **Technology**: Pygame mixer with NumPy-generated waveform

## 🎓 Classroom Application

### Setup Recommendations
1. **Camera Placement**: Position camera to capture students' faces clearly
2. **Lighting**: Ensure adequate lighting for face detection
3. **Distance**: Keep students 0.3m - 0.6m from camera
4. **Angle**: Front-facing view works best

### Multi-Student Monitoring
To monitor multiple students, modify:

```python
max_num_faces=1  # Change to desired number of students
```

### Privacy Considerations
- No video recording by default
- No data storage or transmission
- All processing is local

## 🐛 Troubleshooting

### Camera Not Working
- Ensure camera permissions are granted
- Try changing camera index: `cv2.VideoCapture(1)` or `cv2.VideoCapture(2)`
- Check if another application is using the camera

### Low Detection Accuracy
- Improve lighting conditions
- Clean camera lens
- Reduce distance from camera
- Remove glasses or adjust position

### Alarm Not Playing
- Check system volume
- Verify pygame installation: `pip install --upgrade pygame`
- Check audio output device settings

### High CPU Usage
- Reduce camera resolution
- Increase frame skip rate
- Close other applications

## 📚 References

1. **MediaPipe Face Mesh**: Google's ML solution for facial landmark detection
2. **EAR Method**: Soukupová and Čech (2016) - "Real-Time Eye Blink Detection using Facial Landmarks"
3. **Drowsiness Detection**: Applied in driver safety and classroom monitoring systems

## 🔬 Future Enhancements

- [ ] Add yawning detection using Mouth Aspect Ratio (MAR)
- [ ] Implement head pose estimation for nodding detection
- [ ] Add database logging for attendance and attention tracking
- [ ] Create dashboard for teachers to monitor multiple students
- [ ] Add email/SMS notifications to parents
- [ ] Implement deep learning classifier for improved accuracy
- [ ] Add support for IP cameras
- [ ] Create mobile app version





## 📧 Contact

For questions or support, please open an issue in the repository.

---

