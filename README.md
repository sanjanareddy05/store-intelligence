## Dataset Note

Raw CCTV clips are not included in this repository due to dataset licensing restrictions and repository size limits.

Place the provided CCTV videos inside:

data/videos/

Example:

data/videos/CAM 1.mp4
data/videos/CAM 2.mp4
data/videos/CAM 3.mp4
data/videos/CAM 4.mp4
data/videos/CAM 5.mp4

After placing the clips, run:

python pipeline/detect.py

This generates:

pipeline/output/events.jsonl
