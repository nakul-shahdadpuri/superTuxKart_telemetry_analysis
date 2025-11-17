# SuperTuxKart Telemetry - Frustration Level Analysis

## Overview
This analysis computes game frustration levels for each SuperTuxKart gameplay session based on telemetry data. The frustration score quantifies player difficulty by analyzing off-ground events (when the kart is airborne or off-track).

## Frustration Score Formula

```
FrustrationScore = w₁ · OffGroundRatio + w₂ · AvgOffGroundDuration + w₃ · EventFrequency
```

Where:
- **w₁ = 0.4**: Weight for off-ground ratio
- **w₂ = 0.4**: Weight for average off-ground duration  
- **w₃ = 0.2**: Weight for event frequency

## Metrics Explained

### 1. Off-Ground Ratio
- **Definition**: Percentage of total gameplay time spent off-ground (airborne/off-track)
- **Range**: 0-1 (converted to 0-100%)
- **Interpretation**: Higher values indicate poor track control and more time lost

### 2. Average Off-Ground Duration
- **Definition**: Mean duration (in seconds) of each off-ground event
- **Normalized**: Scaled to 0-1 for fair comparison across sessions
- **Interpretation**: Longer durations suggest difficulty recovering from mistakes

### 3. Off-Ground Event Frequency
- **Definition**: Number of off-ground events per minute of gameplay
- **Normalized**: Scaled to 0-1 for fair comparison
- **Interpretation**: Higher frequency indicates unstable gameplay with frequent disruptions

## Results

### Key Findings
Based on the analysis of 24 gameplay sessions:

**Most Frustrating Sessions:**
1. `telemetry_20251111_221300` (Score: 47.3) - cornfield_crossing track
2. `telemetry_20251111_124504` (Score: 43.1) - cornfield_crossing track
3. `telemetry_20251115_223103` (Score: 40.8) - hacienda track

**Smoothest Sessions:**
- Multiple sessions scored 0.0, indicating perfect ground control throughout gameplay

### Track Analysis
Sessions with frustration scores > 0 show varying difficulty levels:
- **Most challenging tracks**: cornfield_crossing, hacienda
- **Moderate difficulty**: scotland, sandtrack, volcano_island
- **Smoother gameplay**: overworld, abyss

## Generated Files

### Visualizations (PNG)
1. **frustration_score_by_session.png** - Bar chart ranking all sessions by frustration level
2. **frustration_components_breakdown.png** - 4-panel analysis of metric components
3. **most_frustrating_session_timeline.png** - Time series showing ground status and speed
4. **frustration_distribution.png** - Histogram and box plot of score distribution
5. **frustration_by_track.png** - Average frustration comparison across tracks
6. **correlation_heatmap.png** - Correlation matrix of all metrics

### Data Files (CSV)
1. **frustration_analysis_results.csv** - Detailed results for all sessions
2. **frustration_summary_statistics.csv** - Summary statistics

## How to Use for Your Report

### Running the Analysis
1. Open `analysis.ipynb` in Jupyter/VS Code
2. Run all cells sequentially (Cell → Run All)
3. All visualizations and CSV files will be generated automatically

### Report Integration
The generated visualizations are publication-ready:
- **High resolution** (300 DPI)
- **Color-coded** for easy interpretation (green=low frustration, red=high frustration)
- **Labeled axes** with clear titles
- **Professional styling** with seaborn themes

### Customization Options
You can modify the analysis by adjusting:
- **Weights** (w₁, w₂, w₃) in cell 9 to emphasize different aspects
- **Color schemes** in visualization cells
- **Track filtering** to focus on specific gameplay sessions

## Methodology Details

### Event Detection
Off-ground events are detected by:
1. Tracking transitions in the `on_ground` metric (1→0 indicates start, 0→1 indicates end)
2. Calculating duration between start and end of each event
3. Handling edge cases (session ending while off-ground)

### Normalization
To combine metrics fairly:
- Off-ground ratio is already 0-1 scale (percentage)
- Duration and frequency are normalized using min-max scaling
- Final score is scaled to 0-100 for intuitive interpretation

### Statistical Robustness
- Handles sessions of varying lengths (1.5s to 193s)
- Accounts for different track characteristics
- Provides both absolute and normalized metrics

## Interpretation Guide

### Frustration Score Ranges
- **0-20**: Excellent control, minimal disruptions
- **20-40**: Good gameplay with occasional challenges
- **40-60**: Moderate frustration, frequent control issues
- **60-80**: High frustration, significant difficulty
- **80-100**: Extreme frustration, very poor control

### Use Cases
1. **Player Performance Evaluation**: Identify which sessions were most challenging
2. **Track Difficulty Analysis**: Compare average frustration across different tracks
3. **Skill Progression**: Track improvement over time by comparing session dates
4. **Game Design**: Identify problematic track sections for balancing

## Requirements
```python
pandas
numpy
matplotlib
seaborn
```

## Contact & Support
For questions about the analysis methodology or customization, refer to the commented code in `analysis.ipynb`.

---
*Analysis generated on: November 15, 2025*
