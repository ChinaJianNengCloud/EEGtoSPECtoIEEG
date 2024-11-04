#项目的理解和架构
## 原项目的理解
flinkerlab/neural_speech_decoding (github.com)项目是将ECoG的数据转成语音，先用一个ECoGdecoder模型将ECOG与频谱Speech格式对齐，之后计算各种特征，利用伪Speech和频谱Speech和两者的各种声音特征进行loss计算。

## 项目的目的
对浅层的EEG数据进行降噪，降噪的目标是ECoG。
先将EEG数据转成声音，之后利用原项目进行声音转ECOG的操作，即可实现EEG转ECOG(原因，ECOG数据较为难得，利用这个方法可以将EEG转化成ECOG)。


## EEG转声音,见原项目文档

先训练一个声音的自编码器，包含Speechencoder和Speech合成器，中间格式先设置为原项目的格式。

EEG数据通过EEG decoder将数据格式转化成中间格式，之后输入到Speech合成器中合成伪Speech频域数据，之后通过反频域转化即可得到伪Speech

训练好之后将Speech数据先进行频域转化，之后利用decoder将数据格式与自编码器中间形状对齐，最后通过EEGdecoder转化成伪EEG。

在自编码器中用真实EEG与自编码器生成的伪EEG计算l2loss，将自编码器中间数据和伪中间数据计算l2数据

## 声音转ECOG

目前还在进行中，目前使用的是VAE声音生成器，接收的是EEG转声音的中间产物，SPEC(频谱数据),根据这个数据进行训练生成EEG数据。

# 项目的环境
在本地路径local8 F:\sjwlab\chenyinda\naodian_total\env
百度网盘路径 S:\baidu\sjwlab\chenyinda\project\浅层脑电转声音转深层脑电

# 项目代码介绍
module12和moudle34属于第一步，EEG转声音的模型的两个模块，
module12用于训练声音自编码器，
module34用于EEG转声音。

moudle_vae是声音转ECOG模型的模块

1w2w是运行module12的代码

1w2w_inf是推理module12的代码

2e2w是运行moudule34的代码

2e2w_inf是推理module34的代码

start_vae是运行VAE模型的代码

# 当前情况
使用的是数据集N20和N57当作module12模型和module34模型的train
用133当作module12模型和module34模型的val

N20数量有85060
N57数量有1680
133数量有122

数据路径在S:\baidu\sjwlab\chenyinda\project\浅层脑电转声音转深层脑电