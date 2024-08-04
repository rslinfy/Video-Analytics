# Video Analytics Tool using YoloV5 and Streamlit

## 动机
当将模型部署在边缘进行某种监控时，除了深度学习工作外，还需要大量的前端和后端开发——从获取实时数据到显示正确的输出。所以，考虑制作一个小规模的视频分析工具，并分析这种工具的所有功能都有哪些用处，以及可能有哪些局限性。

## 项目组件
1. 配置
2. 推理
3. 结果统计
4. 系统状态
5. 结果总览

## 推理配置
该组件处理工具的所有设置，为您提供输入源（可以是本地视频，rtsp或网络摄像头）、类别 置信度值、漂移检测阈值、fps 下降警告阈值、保存输出视频和保存模型表现不佳的帧的几个选项。

## 推理
这个推理是 YoloV5s 版本 6 的输出，使用 DeepSort 来跟踪对象。我们有标签，然后是类置信度值。在框中我们有对象的 ID。例如，这里有一辆 ID 为 2 的汽车。

## 结果统计
推理统计显示 FPS、当前帧中检测到的物体以及迄今为止检测到的物体总数（未被跟踪）。当 FPS 低于给定阈值时，该工具将发出警报。这可以帮助关注系统的性能，以决定是否升级硬件或优化模型。随着时间的推移，对象的数量可能会慢慢增加，而模型的检测速度会变慢，从而导致 FPS 下降。还可能发生这样的情况：在一天中的某个时间，当对象数量通常会激增时，FPS 会降低，这表明需要优化模型或升级正在使用的硬件。

作为附加功能，我们可以存储在给定时间段内行驶在某条道路上的车辆数量。例如，从早上 6 点到早上 8 点，交通拥堵，因此需要交通监控人员保持警惕。然后早上 8 点之后，交通量减少。这些数据还可以发送给当地机构，帮助他们安排道路维修。

当我们收集数据以重新训练模型时，总检测对象数据也会有所帮助。这个数字可以帮助我们防止阶级不平衡。例如，由于数据漂移，我们想重新训练我们的模型（政府增加了新的电动公交车，其模型与小型货车相混淆，从而导致推断的数据发生变化），因此这个计数可以帮助我们计划我们的训练过程，以防止在一个类别上过度拟合。此外，例如，如果一整天有100辆公共汽车在路上与汽车并排行驶，那么运输机构可以考虑为公共汽车提供一条单独的车道，以帮助调节交通。

## 系统状态
系统统计信息有助于监控 CPU、RAM 和 GPU 的使用情况。它有助于监控硬件是否利用不足或过度。如果当摄像头中物体突然增加时 GPU 利用率频繁达到峰值，则可以决定升级 GPU。同样，这也适用于内存和 CPU。

## 结果总览
在本节中，我们得到推理的摘要，例如 -> 模型表现不佳的类别、检测到至少一个置信度小于阈值的对象的帧数、最小和最大 FPS。

## 主要功能

- 选择本地, RTSP或者Webcam作为视频来源
- 对输入类的阈值进行配置
- 设置FPS下降警告阈值
- 保存推理视频的选项
- 对分类的置信度的配置
- 保存性能较差的帧的选项
- 在当前帧展示目标
- 展示目前为止检测出的所有目标
- 系统状态展示：RAM，CPU和GPU占用
- 展示性能较差的类
- 展示推理期间记录下来的最小和最大的FPS

## 使用方法

1. 克隆这个仓库
2. 安装所有依赖（见requirements.txt）
3. D下载DeepSort的checkpoint[文件](https://drive.google.com/drive/folders/1xhG0kRH1EX5B9_Iz8gQJb7UNnn_riXi6) 然后将其放进 `deep_sort_pytorch/deep_sort/deep/checkpoint`.
4. 使用命令 `streamlit run main.py`来运行程序

<!-- ## Recent Changelog

- Updated the YoloV5s weight file name in the `detect()` function in `app.py`.
- Added a drive link to download the DeepSort checkpoint file (45MB).

## FAQs

- [How to use a custom YoloV5 weight or DeepSort checkpoint file?](https://github.com/SahilChachra/Video-Analytics-Dashboard/issues/5)
- [Unable to use webcam](https://github.com/SahilChachra/Video-Analytics-Dashboard/issues/3)
- [AttributeError: 'Upsample' object has no attribute 'recompute_scale_factor'](https://github.com/ultralytics/yolov5/issues/6948) -->

<!-- ## Extras

Please review the Medium article and consider giving this repository a star.

## Note

The input video should be located in the same folder as `app.py`. If deploying the application on the cloud and using it as a web app, ensure that the user-uploaded video is saved to a temporary folder and pass the path and video name to the appropriate function in `app.py`. This is a known issue with Streamlit. Refer to [StackOverflow](https://stackoverflow.com/questions/65612750/how-can-i-specify-the-exact-folder-in-streamlit-for-the-uploaded-file-to-be-save) for more details. -->
