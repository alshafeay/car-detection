# Real-Time Vehicle Detection, Tracking, and Counting with YOLOv8 and DeepSORT

This project implements a robust system for real-time vehicle detection, tracking, and counting in video streams. It leverages the state-of-the-art YOLOv8 object detection model and the DeepSORT algorithm for persistent object tracking. The system processes a video file, identifies vehicles, assigns a unique ID to each one, and counts them as they cross a designated line.

## Table of Contents

- [Features](#features)
- [How It Works](#how-it-works)
- [Dependencies](#dependencies)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Output](#output)

## Features

-   **High-Accuracy Detection:** Utilizes the YOLOv8 model to accurately detect various types of vehicles (cars, motorcycles, buses, trucks).
-   **Persistent Multi-Object Tracking:** Employs the DeepSORT algorithm to track vehicles across frames, maintaining a consistent ID for each object even with temporary obstructions.
-   **Vehicle Counting:** Implements a virtual line to count vehicles as they pass through a specific point in the video.
-   **Video Processing:** Accepts a video file as input and generates a new, annotated video file showing the tracking boxes, IDs, and the vehicle count.
-   **User-Friendly:** A simple file dialog allows for easy selection of the video to be processed.

## How It Works

The processing pipeline follows these steps:

1.  **Video Input:** The user is prompted to select a video file through a file dialog.
2.  **Object Detection:** Each frame of the video is passed to the YOLOv8 model, which identifies and returns bounding boxes for all detected vehicles.
3.  **Object Tracking:** The detected bounding boxes are fed into the DeepSORT tracker. DeepSORT assigns a unique `track_id` to each new vehicle and updates the location of existing vehicles in subsequent frames.
4.  **Counting Logic:** A horizontal line is drawn on the frame. The system checks the position of each tracked vehicle. If a vehicle's center point crosses this line, the total count is incremented, and its ID is stored to prevent recounting.
5.  **Visualization & Output:** The processed frames, complete with bounding boxes, tracking IDs, the counting line, and the total vehicle count, are displayed in real-time and written to a new video file.

## Dependencies

The project requires Python 3 and the following libraries:

-   `opencv-python`
-   `ultralytics` (for YOLOv8)
-   `deep-sort-realtime`
-   `numpy`
-   `tkinter` (usually included with standard Python installations)

## Installation

1.  **Clone or download the project files.**

2.  **Install the required Python libraries using pip.** Open your terminal or command prompt and run the following command:
    ```sh
    pip install opencv-python ultralytics deep-sort-realtime
    ```
    *Note: `numpy` and `tkinter` are typically installed as dependencies of the libraries above.*

3.  **YOLOv8 Model:** The `yolov8m.pt` model weights will be downloaded automatically by the `ultralytics` library the first time you run the script. No manual download is necessary.

## Usage

1.  Open the `car_detection_project.ipynb` file in a Jupyter Notebook environment (like Jupyter Lab or Visual Studio Code).
2.  Run the cells of the notebook sequentially from top to bottom.
3.  When you execute the final cell (`process_video()`), a file dialog window will appear.
4.  Select the video file you wish to process.
5.  A new window titled "Vehicle Tracking" will open, showing the real-time detection and tracking.
6.  To stop the processing before the video ends, make sure the "Vehicle Tracking" window is active and press the **'q'** key.
7.  Once the video is fully processed, the application will close automatically.

## Configuration

You can modify the following parameters in the `process_video` function within the notebook to suit your needs:

-   `line_position`: Change the integer value (default is `300`) to move the vehicle counting line up or down.
-   `score`: Adjust the confidence threshold (default is `0.4`) to filter out less certain detections.
-   `int(class_id) in [2, 3, 5, 7]`: Modify this list of class IDs to detect different types of objects. (Common COCO dataset IDs: 2=car, 3=motorcycle, 5=bus, 7=truck).

## Output

-   **Real-Time Display:** A window showing the live tracking process.
-   **Processed Video:** A new video file is saved in the same directory as the input video, with `_processed.mp4` appended to its name.
-   **Console Log:** The terminal will display the path of the video being processed, and upon completion, it will print the total number of vehicles counted and the path to the saved output video.
