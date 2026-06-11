# YOLO Object Detection for Bakery Checkout

## Context
Used in [[projects/final-report/README|final-report]] for real-time product recognition at a bakery checkout counter.

## Implementation
- YOLOv8n trained on 6 bakery products
- OpenCV tray-color classification (green = regular, orange = discount zone)
- FIFO inventory deduction on checkout

## Key Decisions
- YOLOv8n chosen for speed over accuracy (real-time checkout)
- Tray color provides secondary validation to reduce misdetection

## Limitations (Pre-Field-Test)
- Trained on synthetic/static images only
- Not yet tested under real bakery lighting and occlusion

## References
- See related literature in `literature/Applied robotics/`
