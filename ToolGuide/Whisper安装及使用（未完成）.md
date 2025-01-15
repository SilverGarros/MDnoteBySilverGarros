# Whisper——OpenAI开源离线语音识别工具安装及使用

## whisper简单介绍

Open AI在2022年9月21日开源了号称其英文语音辨识能力已达到人类水准的Whisper神经网络，且它亦支持其它98种语言的自动语音辨识。 Whisper系统所提供的自动语音辨识（Automatic Speech Recognition，ASR）模型是被训练来运行语音辨识与翻译任务的，它们能将各种语言的语音变成文本，也能将这些文本翻译成英文。

Whisper仓库地址：

## 前置环境安装

- ffmpeg

- git

- Pytorch



#### 下载ffmpeg并添加至环境变量

#### 下载git并添加至环境变量

#### 安装Pytorch

## Whisper的安装

Whisper仓库地址：

#### 1.先运行

``` cmd
pip install git+https://github.com/openai/whisper.git
```

#### 2.再运行

``` cmd
pip install --upgrade --no-deps --force-reinstall git+https://github.com/openai/whisper.git
```

完成whisper的安装

#### 注意：如果将Pytorch安装在Conda环境内，则要在Conda环境内运行上面安装指令，且Whisper后续也要在Conda环境内进行使用