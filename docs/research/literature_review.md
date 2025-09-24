# Deepfake Detection Literature Review

## Day 1: FaceForensics++ Analysis

**Paper**: "FaceForensics++: Learning to Detect Manipulated Facial Images" (Rössler et al., 2019)

### Key Technical Findings:
- Dataset: 1,000 original videos, 4,000 manipulated videos
- Methods evaluated: Face2Face, FaceSwap, Deepfakes, NeuralTextures
- Best performance: ~95% accuracy on compressed videos
- CNN architectures: ResNet, Xception showed strong performance
- Critical preprocessing: Face detection and alignment essential

### Implementation Insights:
- MTCNN effective for face detection pipeline
- Data augmentation crucial for robustness
- Compression artifacts significantly impact performance
- Frame-level vs video-level classification tradeoffs

## Day 2: DFDC Dataset Analysis  

**Paper**: "The DeepFake Detection Challenge (DFDC) Dataset" (Dolhansky et al., 2020)

### Dataset Characteristics:
- Scale: 128,154 videos with 4.6M faces
- Demographic diversity: 3,426 paid actors across demographics
- Technical specs: Variable compression, resolution, lighting
- Challenge results: Best accuracy ~65% (lower than FaceForensics++)

### Key Challenge Insights:
- Cross-dataset generalization is difficult
- Ensemble methods outperformed single models
- Temporal consistency features improved results
- Real-world conditions significantly harder than controlled datasets

### Comparison Summary:

| Aspect | FaceForensics++ | DFDC |
|--------|----------------|------|
| Scale | 1K original videos | 23K real videos |
| Diversity | Limited actors | High demographic diversity |
| Controlled Environment | Yes | No - realistic conditions |
| Best Accuracy | ~95% | ~65% |
| Main Challenge | Compression artifacts | Generalization |

## Technical Architecture Decisions

Based on literature analysis:

### Recommended Approach:
1. **Face Detection**: MTCNN for preprocessing, MediaPipe for real-time
2. **CNN Architecture**: EfficientNet-B4 as backbone (good accuracy/efficiency balance)
3. **Training Strategy**: Transfer learning from ImageNet → Fine-tune on FaceForensics++ → Validate on DFDC subset
4. **Temporal Features**: Frame sequences analysis for consistency checking

### Performance Targets:
- Accuracy: >85% on controlled data, >70% on realistic conditions
- Speed: <2 seconds per frame processing
- Memory: <8GB training, <4GB inference