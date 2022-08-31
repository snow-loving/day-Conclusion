入门指南官网地址：https://developer.nvidia.com/deepstream-sdk 

英伟达github项目地址：https://github.com/orgs/NVIDIA-AI-IOT/

torch2trt项目地址：https://github.com/NVIDIA-AI-IOT/torch2trt

整个应用程序是由一连串的GStreamer管道（pipeline）组成，从视频流数据输入，然后处理流的元素或插件以及最后的输出流构成整个流程

插件，有一个输入sink和一个输出source。管道中一个插件的source pad可以链接到下一个插件的sink pad，源包括处理提取的信息、元数据，用于视频注视和输入流的其他细节。      

***整个工作流程就是：输入/计算处理/汇总输出***

deepstream配置文件config中为模型推理设置文件

``` python
├── labels_cancer.txt    #labls为分类标签文件设置
├── labels_flush.txt		 #config文件为参数设置
├── labels_position12.txt
├── labels_position38.txt
├── tr_cancer_config.txt
├── tr_flush_config.txt
└── tr_position_config.txt
```

### **工作流程：**https://docs.nvidia.com/metropolis/deepstream/5.1/dev-guide/text/DS_Overview.html

1. 首先数据流通过网络或文件系统或者摄像机，使用cpu捕捉流，然后进入内存，被nvdec加速器进行解码。解码的工具为gst-nvvdieo4linux2

2. 解码后可以进行图像的预处理，有颜色转换/扭曲等插件。

3. 批处理帧，Gst-nvstreammux插件获得最佳性能

4. 发送推理，可以使用推理加速器tensorRT等相关框架，TensorRT 推理是使用Gst-nvinfer插件执行的，使用 Triton 的推理是使用Gst-nvinferserver插件完成的。推理可以为 Jetson AGX Xavier 和 Xavier NX 使用 GPU 或 DLA（深度学习加速器）

5. 跟踪对象（gst-nvtracker插件）

6. 创建可视化工件 例如边界框/分割掩码/标签（Gst-nvdsosd可视化插件）

7. 输出结果

   ### 参考应用

   deepstream- test1-test4 4个案例可以进行应用
   deepstream5.1为目前我们所需要的代码，可以进行推理

---
deepstrem 编译部署项目文件存放位置

```
.tianru/configs/
包含engine文件6个。包含配置文件3个。包含3个label标签文件

然后进入文件夹deepstream里面
```
   
               
