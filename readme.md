Here is the documentation (README.md) for your code:

---

# Road width calculation using Vehicle Detection and Tracking with YOLOv8

## Overview

This project implements Road width calculation using Vehicle Detection and Tracking in a video using the YOLOv8 model. The video is processed frame by frame to detect vehicles (cars and trucks), calculate their positions, and estimate the road width based on the detected vehicles' positions. The results, including the detected vehicles and calculated road widths, are displayed in the video and saved to a text file.

## Requirements

- Python 3.7+
- OpenCV (`opencv-python`)
- NumPy (`numpy`)
- Ultralytics YOLOv8 (`ultralytics`)
- SciPy (`scipy`)

You can install the required dependencies using the following command:

```bash
pip install opencv-python numpy ultralytics scipy
```

## Files

- `vehicle_detection_tracking.ipynb`: Main script for vehicle detection and road width calculation.
- `road_width_results.txt`: Output text file where the calculated road widths are saved.

## Functionality

1. **YOLOv8 Model**: The script loads a YOLOv8 model (`yolov8n.pt`) for detecting vehicles. It detects objects of classes corresponding to cars and trucks.
2. **Video Processing**: The script processes each frame of a given video (`video.mp4`), detects vehicles, and computes the width of the detected road segments.
3. **Road Regions**: The video is divided into manually specified road regions, and vehicle centroids are tracked within each region.
4. **Mapping Pixel to Real World**: Using a scale factor (set to 0.05), the script converts pixel distances between detected vehicles to real-world distances (in meters).
5. **Results**: The detected vehicle positions are highlighted with bounding boxes, centroids are marked, and the width of the road is calculated based on the furthest distance between two centroids within a road region.
6. **Output**: The results, including the road width for each frame, are saved to a text file (`road_width_results.txt`), and the processed frames are displayed in a window. The script stops if 'q' is pressed.

## Parameters

- **`video_path`**: Path to the input video file. Default is `"video.mp4"`.
- **`scale_factor`**: The factor used to convert pixel distance to real-world distance (in meters). Default is `0.05`.

### Preprocessing Steps

1. **Resize**: The frame is resized to maintain the original dimensions.
2. **Noise Reduction**: A Gaussian blur is applied to the frame to reduce noise.
3. **Perspective Transformation**: A bird's-eye view transformation is applied to the frame using source and destination points.

### Vehicle Detection

- The YOLOv8 model detects vehicles of classes `2` (cars) and `7` (trucks).
- The detected bounding boxes are drawn around vehicles, and centroids are marked.

### Road Width Calculation

For each road region:

- Centroids of detected vehicles are calculated.
- The distance between the furthest centroids within the region is calculated.
- The pixel distance is converted to real-world distance using the scale factor.
- The road width is displayed and saved.

## Example Usage

1. **Prepare your video file**: Ensure your video is named `video.mp4` or modify the `video_path` variable to the correct path.
2. **Run the script**: Execute the Python script:

   ```bash
   python vehicle_detection_tracking.py
   ```

3. **Viewing the output**: The processed video will be displayed in a window with vehicle detection and road width estimation. The results for each frame will be saved in the file `road_width_results.txt`.

4. **Exit**: Press 'q' to stop the video playback.

## Calibration and Adjustments

- **Scale Factor**: Adjust the `scale_factor` depending on the real-world dimensions of the road and vehicles in your video.
- **Road Regions**: The `road_regions` variable defines the regions of the video for road width calculation. Modify these values to fit your video.

## Output Example

The `road_width_results.txt` file will contain the following format:

```
Frame 1:
  Road 1: 5.67 meters
  Road 2: 8.32 meters
  Road 3: 6.45 meters
```

## Acknowledgements

- The project uses the YOLOv8 model for vehicle detection.
- OpenCV is used for video processing and display.
- SciPy is used for calculating the Euclidean distance between centroids.

This README.md provides an overview of the project, setup instructions, and detailed usage for the code. Let me know if you need any more adjustments or additional features!
