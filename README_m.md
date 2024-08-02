# Video Analytics Tool using YoloV5 and Streamlit

## Motivation
In the field of AI, the analysis and visualization of data are crucial. To enhance the understanding of inference results, it is essential to display this data effectively on a platform. Deploying a model for monitoring purposes involves extensive frontend and backend development beyond just deep learning efforts, including tasks such as acquiring live data and presenting accurate outputs. This project aims to create a small-scale video analytics tool to explore useful features and identify potential limitations.

## Demo

[Demo Video](https://user-images.githubusercontent.com/37156032/160282244-42f6bd8c-bfc8-47af-8973-d3d199140e44.mp4)

## Features

For comprehensive insights, please refer to my [Medium Blog](https://sahilchachra.medium.com/video-analytics-dashboard-for-yolov5-and-deepsort-c5994461cb44).

- Selection of input source: Local, RTSP, or Webcam
- Configuration of input class threshold
- Setting FPS drop warning threshold
- Option to save inference video
- Configuration of class confidence for drift detection
- Option to save poorly performing frames
- Display of objects in the current frame
- Display of total detected objects so far
- System statistics display: RAM, CPU, and GPU usage
- Display of the poorly performing class
- Display of minimum and maximum FPS recorded during inference

## How to Use

1. Clone this repository.
2. Install all necessary dependencies.
3. Download the DeepSort checkpoint file from [this link](https://drive.google.com/drive/folders/1xhG0kRH1EX5B9_Iz8gQJb7UNnn_riXi6) and place it in `deep_sort_pytorch/deep_sort/deep/checkpoint`.
4. Run the application using the command: `streamlit run app.py`.

## Recent Changelog

- Updated the YoloV5s weight file name in the `detect()` function in `app.py`.
- Added a drive link to download the DeepSort checkpoint file (45MB).

## FAQs

- [How to use a custom YoloV5 weight or DeepSort checkpoint file?](https://github.com/SahilChachra/Video-Analytics-Dashboard/issues/5)
- [Unable to use webcam](https://github.com/SahilChachra/Video-Analytics-Dashboard/issues/3)
- [AttributeError: 'Upsample' object has no attribute 'recompute_scale_factor'](https://github.com/ultralytics/yolov5/issues/6948)

## Extras

Please review the Medium article and consider giving this repository a star.

## Note

The input video should be located in the same folder as `app.py`. If deploying the application on the cloud and using it as a web app, ensure that the user-uploaded video is saved to a temporary folder and pass the path and video name to the appropriate function in `app.py`. This is a known issue with Streamlit. Refer to [StackOverflow](https://stackoverflow.com/questions/65612750/how-can-i-specify-the-exact-folder-in-streamlit-for-the-uploaded-file-to-be-save) for more details.
