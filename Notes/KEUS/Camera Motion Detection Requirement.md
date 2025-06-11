This is a Python-based motion detection system that processes RTSP camera streams, detects motion, and records video chunks when motion is detected. The system provides both HTTP APIs and WebSocket real-time notifications.

### **Key Components:**

#### **1. Docker Configuration**

- **Dockerfile**: Based on Python 3.11-slim with OpenCV dependencies, FFmpeg for video processing, Node.js for PM2 process management
- **[entrypoint.sh](vscode-file://vscode-app/c:/Users/keusu/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Uses PM2 to manage the Python application
- **[ecosystem.config.js](vscode-file://vscode-app/c:/Users/keusu/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: PM2 configuration to run the main Python script
- **[requirements.txt](vscode-file://vscode-app/c:/Users/keusu/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html)**: Dependencies include OpenCV, requests, websockets, and psutil

#### **2. Main Application

- Entry point that orchestrates the entire system
- Low CPU-Usage, below 5% atmax
- Starts WebSocket server, camera manager, and HTTP API server
- Handles graceful shutdown with signal handlers
- Provides command-line argument parsing for host/port configuration

#### **3. Camera Management

- **CameraWorker**: Individual threaded workers for each camera
- **CameraManager**: Thread-safe management of multiple cameras
- Features:
    - RTSP stream processing with OpenCV
    - Motion detection integration
    - Automatic video recording with chunking (60-second chunks)
    - Performance monitoring and adaptive frame processing
    - Graceful camera start/stop operations

#### **4. Motion Detection
- Computer vision-based motion detection using OpenCV
- Features:
    - Frame differencing with Gaussian blur
    - Configurable threshold and minimum area parameters
    - Adaptive sleep timing to optimize CPU usage
    - Performance statistics tracking
    - Frame skipping for efficiency (processes every 10th frame)

#### **5. Video Recording

- FFmpeg-based video recording from RTSP streams
- Optimized settings for low CPU usage:
    - H.264 encoding with ultrafast preset
    - Limited resolution (1280x720) and frame rate (15 FPS)
    - AAC audio encoding
    - TCP transport for reliability

#### **6. WebSocket Server

- Real-time motion detection event broadcasting
- Features:
    - Client connection management
    - Ping/pong heartbeat handling
    - Motion start/stop event notifications
    - Resilient client handling (never removes clients on errors)

#### **7. HTTP API

- RESTful API for camera management
- Endpoints:
    - `POST /addCamera`: Add new camera with camera_id and rtsp_url
    - `DELETE /deleteCamera?camera_id=ID`: Remove camera
    - `GET /status`: Get system and camera status
- CORS-enabled for web client integration

#### **8. Configuration

- Centralized configuration for all system parameters
- Key settings:
    - Motion detection thresholds and timing
    - Video recording quality and performance settings
    - Server ports and network configuration
    - File system paths and cleanup policies
#### **9. Utilities

- Recording directory management
- Automatic cleanup of old recordings (3-day retention)
- Filename generation for video chunks

### **Key Features:**

1. **Multi-Camera Support**: Thread-safe management of multiple RTSP cameras
2. **Motion Detection**: Efficient OpenCV-based detection with configurable sensitivity
3. **Smart Recording**: Only records when motion is detected, with configurable post-motion buffer
4. **Video Chunking**: Creates 60-second video segments for easier management
5. **Real-time Notifications**: WebSocket events for motion start/stop
6. **RESTful API**: Easy integration for adding/removing cameras
7. **Performance Optimization**: Adaptive frame processing, CPU-optimized encoding
8. **Automatic Cleanup**: Manages disk space by removing old recordings
9. **Graceful Shutdown**: Proper resource cleanup on system termination

### **Default Configuration:**

- Motion detection resolution: 128x96 (optimized for performance)
- Video recording: 1280x720 @ 15 FPS
- API server: Port 8083
- WebSocket server: Port 8084
- Recording chunks: 60 seconds each
- Post-motion buffer: 3 seconds
- Cleanup retention: 3 days