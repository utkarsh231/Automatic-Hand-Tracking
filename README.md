# Automatic Hand Tracking

This repository contains a Python script for processing video frames and applying segmentation techniques based on hand detection. The segmentation results are rendered and saved into a new video file.

## Features
- Detects hand coordinates in video frames using a provided `get_hand_coordinates()` function.
- Performs segmentation using a predictor object.
- Propagates segmentation results across video frames.
- Visualizes segmentation masks and overlays them on video frames.
- Outputs the final video with segmentation overlays.

## Requirements
To run the script, you need the following:

- Python 3.7+
- Required Python libraries:
  - `numpy`
  - `matplotlib`
  - `opencv-python`
  - `Pillow`
  - `torch`
  - `mediapipe`

Install the dependencies using pip:
```bash
pip install numpy matplotlib opencv-python Pillow mediapipe torch
```

You also need to install to [sam2](https://github.com/facebookresearch/sam2?tab=readme-ov-file) which is described in the main.ipynb on how to do so. 

## Usage

1. **Input Video Frames**:
   Ensure your video frames are stored as images in a directory, sorted in ascending order by frame index (e.g., `00001.jpg`, `00002.jpg`, etc.). You can use ffmpeg to convert your video file to frames.

2. **Prepare the Input Functions and Objects**:
   - Implement or provide the `get_hand_coordinates()` function, which extracts the coordinates of hands from a specified frame.
   - Provide a predictor object with methods for segmentation and propagation.
   - Initialize the predictor's inference state.

3. **Run the Script**:
   Call the `process_video_with_segmentation()` function from the provided script.

  `process_video_with_segmentation(
    video_dir="/path/to/video_frames",
    get_hand_coordinates=get_hand_coordinates,
    predictor=predictor,
    inference_state=inference_state,
    output_video_path="segmented_output.mp4"
    )
  `
   Also, make sure to give correct file path at the beginning of Task 1  and the end of the script.

4. **Output**:
   The segmented video will be saved at the specified path (default: `segmented_output.mp4`).

## Functionality Overview

### `process_video_with_segmentation()`
This is the main function that processes the video frames, applies segmentation, and outputs the final video.

#### Arguments:
- `video_dir` (str): Path to the directory containing video frames.
- `get_hand_coordinates` (function): Function to get hand coordinates from a frame.
- `predictor` (object): Predictor object for segmentation.
- `inference_state` (object): Inference state for the predictor.
- `output_video_path` (str, optional): Path to save the output video (default: `"output.mp4"`).
- `vis_frame_stride` (int, optional): Visualization stride for rendering frames (default: `30`).

#### Steps:
1. Extracts hand coordinates from the first frame using `get_hand_coordinates()`.
2. Adds points for segmentation based on hand coordinates.
3. Propagates segmentation masks across video frames using the predictor.
4. Renders the segmentation results on frames and compiles them into a video.


## License
This project is licensed under the MIT License. Feel free to use and modify the code as needed.

