# Pruning-caffemodel-using-L1
使用论文 PRUNING FILTERS FOR EFFICIENT CONVNETS 提到的方法，深度学习框架使用caffe
目前只支持resnet类似结构（只有sphereface20 和sphereface64），使用vggface2进行剪切后的微调，微调后的压缩模型在lfw上可以到99.4%
具体使用请直接运行network_compression.exe即可，具体配置config文件如下：
[LoseWeight]
Isweightloss=0    // 如设为1 则不进行压缩，只按照prototxt文件网络对caffemodel文件进行剪切，去掉前向传播不用的参数

[Logdisplay]
Islogdisplay=0    // 设为1 则会打印相关信息

[Sphereface20]
IsPruned=1        // 和sphereface64 的IsPruned值不能同时为1
Ta_pruning_ratio=0.,0.,0.7,0.5    //模型中的con1-1 ，2-1 ，3-1 ，4-1层等
Tb_pruning_ratio=0.,0.,0.,0.95,0.95,0.95,0.95,0.95  // 模型中的1-2，2-2，2-4层等
Ip_pruning_ratio=0.75   // ip层的压缩参数，不能为1，越大压缩越多

[Sphereface64]
IsPruned=0
Ta_pruning_ratio=0.,0.,0.7,0.7
Tb_pruning_ratio=0.0,0.0,0.0,0.5,0.5,0.5,0.5,0.5,0.5,0.5,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9
Ip_pruning_ratio=0.5

[FilePath]
Srcmodelfile=model/MobileFaceNet_deploy.prototxt  //输入网络文件  
Srcweightsfile=model/AMS_s30m35__iter_300000.caffemodel // 输入权重文件
Dstmodelfile=   // 默认当前位置
Dstweightsfile= // 默认当前位置



