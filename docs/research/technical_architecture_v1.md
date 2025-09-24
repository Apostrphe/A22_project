# Technical Architecture Plan - Member A Components

## Computer Vision Pipeline Architecture

### 1. Face Detection Module
**Primary**: MTCNN (Multi-task CNN)
- High accuracy face detection and landmark extraction
- Good for preprocessing pipeline
- Used in most literature benchmarks

**Secondary**: MediaPipe
- Real-time performance for live demo
- Mobile-optimized for deployment

### 2. Video Preprocessing Pipeline
```python
# Planned pipeline structure
def video_preprocessing_pipeline(video_path):
    frames = extract_frames(video_path, fps=30)
    faces = detect_faces(frames)  # MTCNN
    normalized_faces = normalize_faces(faces, size=(224,224))
    quality_filtered = filter_low_quality(normalized_faces)
    return quality_filtered