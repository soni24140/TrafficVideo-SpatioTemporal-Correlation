Correlation System Spatial–Temporal



Introduction




This project computes spatial, temporal, and exact-time Spearman correlation between video regions (tiles/segments). Each video is divided into multiple segments, and the system identifies which regions are highly correlated and at what exact time.
All results—heatmaps, correlation matrices, movement plots, temporal variation graphs, and timestamp reports—are stored under: comprehensive_temporal_results/




1 Directory Structure:


 
TileClipper_Implementation/
│
├── correlation.main.py          # Main class file (SpatialTemporalCrossCorrelation)
│
├── data/
│     └── video/                 # Input videos
│          ├── cam1.mp4
│          ├── cam2.mp4
│          └── ...
│
└── comprehensive_temporal_results/      # Output directory (auto-created)
       ├── spatial_temporal_results/
       │        ├── movement_matrix.csv
       │        ├── temporal_delay_results.json
       │        └── region_movement_plots/
       │
       └── exact_time_correlation/
                ├── heatmap_time_windows.png
                ├── heatmap_region_pairs.png
                ├── heatmap_correlation_distribution.png
                └── time_window_report.txt




2 Dependencies



All experiments are developed and tested on:

Windows 10 / Windows 11

Ubuntu 20.04 / 22.04

Python 3.8 – 3.10

Your correlation system uses standard Python libraries for:

Video processing

Statistical correlation

Plotting

Handling time-series

Saving heatmaps and reports





3 Creating Python Environment



$> git clone https://github.com/soni24140/TrafficVideo-SpatioTemporal-Correlation.git
$> cd TileClipper
$> git submodule update --init --recursive
$> pip3 install virtualenv                  
$> python3 -m virtualenv env
$> source env/bin/activate                       # for bash
(env) $> pip3 install -r src/requirements.txt    # installs python libraries





4 Input Videos / Dataset Preparation



Your system works on raw normal videos (not tiled videos).
Each video is divided internally into spatial regions (tiles/segments) and then analyzed.

Place your videos inside the following directory:

videos/
    └── TestDataset/
            └── sample_video.mp4




There is no need for tile groundtruths, special encoders, or calibration files.
The system automatically:



extracts frames

divides them into regions

computes Spearman spatial & temporal correlations

detects timestamps where two regions highly correlate





5) Running the Correlation System on a Sample Video



The main entry script is:

src/correlation_main.py


Run the system on a sample video:

(env) $> python3 src/correlation_main.py \
        --video-folder videos/TestDataset/ \
        --output-dir comprehensive_temporal_results

After execution, the following outputs will be created:

Inside:

comprehensive_temporal_results/


You will find:

Output Type	Description
spatial_heatmaps/	Spearman spatial correlation heatmap for each segment
temporal_correlation_plots/	Region-vs-region temporal correlation curves
exact_time_correlation/	CSV files containing timestamps where two regions are most correlated
region_stats.json	Additional region-level statistics
logs/	Runtime logs




6) Reproducing Results



All correlation results (heatmaps, time-series, CSVs) are stored inside the output directory.

To regenerate the complete set of results, simply re-run:

python3 src/correlation_main.py --video-folder videos/ --output-dir comprehensive_temporal_results/


This will recompute correlations for all videos in the folder.

Running again overwrites previous output inside the comprehensive_temporal_results/ directory.



Running Experiments




Below are steps equivalent to TileClipper's format but adapted to your correlation system.

1) Region Segmentation (Internal Step)

Unlike TileClipper, you do not need external tile encoders.

Your system automatically segments each frame into regions:

4×4 (default)

or configurable inside the class (num_segments)

This step is performed internally by:

SpatialTemporalCrossCorrelation.generate_segments()


No user action is needed.




2) Computing Spearman Spatial Correlation
   

Spatial correlation is computed between all segments of the same frame.

Internal call:

compute_spatial_spearman_correlation()




Outputs saved to:

output/spatial_heatmaps/




3) Computing Spearman Temporal Correlation

Temporal correlation is computed region-wise across all frames.

Internal call:

compute_temporal_correlation()


Outputs saved to:

output/temporal_correlation_plots/



4) Exact-Time High Correlation Detection

This step finds at which specific timestamps two regions behave similarly (high correlation).

Internal call:

compute_exact_time_correlation()


Outputs saved to:

output/exact_time_correlation/region_pair_timestamp_report.csv


Contains:

region A

region B

timestamp

correlation strength




5) Batch Processing All Videos

To run correlation analysis on all videos inside videos/:

(env) $> python3 src/runCorrelationOnAllVideos.py




This script:

reads all videos

runs spatial + temporal correlation

generates exact-time reports

saves combined logs

Equivalent to TileClipper’s “runTileClipperOnAllVideos”.




6) Generating Summary Reports

After running the system on all videos:

(env) $> python3 src/generateSummaryReports.py




This will create:

aggregated region statistics

combined temporal patterns

a merged CSV file for all high-correlation timestamps

Outputs saved to:

output/summary_reports/


