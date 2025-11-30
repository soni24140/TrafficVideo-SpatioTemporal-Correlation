# Traffic Video Spatio-Temporal Correlation Analysis

## Overview
This project implements a comprehensive spatial-temporal correlation analysis system for traffic video data. The system automatically processes raw video footage, divides frames into spatial regions, and computes Spearman correlations to identify relationships between different areas across time. This enables detection of coordinated movement patterns, traffic flow dependencies, and temporal delays between regions.

## Key Features
- **Spatial Correlation Analysis**: Identifies relationships between different regions within the same frame
- **Temporal Correlation Analysis**: Tracks how regions correlate across time sequences
- **Exact-Time Correlation Detection**: Pinpoints specific timestamps where regions show high correlation
- **Automated Region Segmentation**: Divides frames into configurable grid segments (default 4×4)
- **Comprehensive Visualization**: Generates heatmaps, movement plots, and temporal variation graphs
- **Batch Processing**: Supports analysis of multiple videos in sequence

## Repository Structure
<img width="699" height="645" alt="image" src="https://github.com/user-attachments/assets/a57b79f9-5876-486c-b564-74695a81ac6f" />

## Installation & Setup

### Prerequisites
- **Operating Systems**: Windows 10/11, Ubuntu 20.04/22.04
- **Python**: Version 3.8 - 3.10

### Environment Setup
```bash
# Clone repository
git clone https://github.com/soni24140/TrafficVideo-SpatioTemporal-Correlation.git
cd TrafficVideo-SpatioTemporal-Correlation

# Create and activate virtual environment
python3 -m virtualenv env
source env/bin/activate  # On Windows: env\Scripts\activate

# Install dependencies
pip install -r requirements.txt

## Usage

### Basic Single Video Analysis
```bash
python src/correlation_main.py \
    --video-folder data/videos/TestDataset/ \
    --output-dir comprehensive_temporal_results
```

### Batch Processing Multiple Videos
```bash
python src/runCorrelationOnAllVideos.py
```

### Generating Summary Reports
```bash
python src/generateSummaryReports.py
```

---

## Input Data Preparation

Place your input videos in:

```
data/videos/TestDataset/
├── cam1.mp4
├── cam2.mp4
└── ...
```

---

## Output Documentation

### Primary Outputs
- **Spatial Correlation Heatmaps** – Spearman correlation between regions within frames
- **Temporal Correlation Plots** – Region-vs-region correlation across time sequences
- **Exact-Time Correlation Reports** – Timestamps of high correlation
- **Region Statistics** – Numerical summaries for each region

### Visualization Outputs
- heatmap_time_windows.png – Time-window correlation patterns
- heatmap_region_pairs.png – Pairwise region correlation strengths
- heatmap_correlation_distribution.png – Overall correlation distribution
- Movement matrices and temporal delay visualizations

---

## Methodology

### Region Segmentation
- Frames divided automatically into a **4×4 grid** (default)
- Grid size configurable using the **num_segments** argument

### Correlation Computation
- **Spatial Correlation**: Spearman correlation within frames
- **Temporal Correlation**: Correlation across time sequences
- **Exact-Time Correlation Detection**: Identifies timestamps with strong correlations

---

## Reproducing Results
```bash
python src/correlation_main.py \
    --video-folder data/videos/ \
    --output-dir comprehensive_temporal_results
```

---

## Technical Specifications
- **Video Formats Supported**: MP4, AVI, MOV
- **Performance**: Optimized for large video datasets
- **Memory Efficiency**: Stream-based frame processing
- **Scalability**: Works with high-resolution video

---

## Support
For help or troubleshooting:
- Check logs at: `comprehensive_temporal_results/logs/`
- Review example outputs in the repository
- Open a GitHub Issue with detailed description

---

## License







