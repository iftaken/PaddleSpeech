# PaddleSpeech 语音合成

## 效果演示

##### 语音合成

<div align = "center">
<table style="width:100%">
  <thead>
    <tr>
      <th width="550">输入文本</th>
      <th>合成音频</th>
    </tr>
  </thead>
  <tbody>
   <tr>
      <td >Life was like a box of chocolates, you never know what you're gonna get.</td>
      <td align = "center">
      <a href="https://paddlespeech.bj.bcebos.com/Parakeet/docs/demos/tacotron2_ljspeech_waveflow_samples_0.2/sentence_1.wav" rel="nofollow">
            <img align="center" src="./docs/images/audio_icon.png" width="200" style="max-width: 100%;"></a><br>
      </td>
    </tr>
    <tr>
      <td >早上好，今天是2020/10/29，最低温度是-3°C。</td>
      <td align = "center">
      <a href="https://paddlespeech.bj.bcebos.com/Parakeet/docs/demos/parakeet_espnet_fs2_pwg_demo/tn_g2p/parakeet/001.wav" rel="nofollow">
            <img align="center" src="./docs/images/audio_icon.png" width="200" style="max-width: 100%;"></a><br>
      </td>
    </tr>
    <tr>
      <td >季姬寂，集鸡，鸡即棘鸡。棘鸡饥叽，季姬及箕稷济鸡。鸡既济，跻姬笈，季姬忌，急咭鸡，鸡急，继圾几，季姬急，即籍箕击鸡，箕疾击几伎，伎即齑，鸡叽集几基，季姬急极屐击鸡，鸡既殛，季姬激，即记《季姬击鸡记》。</td>
      <td align = "center">
      <a href="https://paddlespeech.bj.bcebos.com/Parakeet/docs/demos/jijiji.wav" rel="nofollow">
            <img align="center" src="./docs/images/audio_icon.png" width="200" style="max-width: 100%;"></a><br>
      </td>
    </tr>
  </tbody>
</table>

</div>

更多合成音频，可以参考 [PaddleSpeech 语音合成音频示例](https://paddlespeech.readthedocs.io/en/latest/tts/demo.html)。

## 安装

PaddleSpeech 安装请参考 主页 Readme 中[【安装】](https://github.com/PaddlePaddle/PaddleSpeech/blob/develop/README_cn.md#%E5%AE%89%E8%A3%85)部分，请确保 PaddleSpeech 安装完整。

## 快速开始

输出 24k 采样率 wav 格式音频

### 命令行

```bash
paddlespeech tts --input "你好，欢迎使用百度飞桨深度学习框架！" --output output.wav
```

`--help` 参数，获取使用说明列表（包含支持的模型列表）

```bash
paddlespeech tts --help
```

部分参数说明

+ `--help` , `-h`         show this help message and exit
+ `--input` INPUT         Input text to generate.
+ `--am` Choose acoustic model type of tts task.
+ `--am_config` AM_CONFIG Config of acoustic model. Use deault config when it is None.
+ `--am_ckpt` AM_CKPT     Checkpoint file of acoustic model.
+ `--am_stat` AM_STAT     mean and standard deviation used to normalize spectrogram when training acoustic model.
+ `--phones_dict` PHONES_DICT phone vocabulary file.
+ `--tones_dict` TONES_DICT tone vocabulary file.
+ `--speaker_dict` SPEAKER_DICT speaker id map file.
+ `--spk_id` SPK_ID       spk id for multi speaker acoustic model
+ `--voc`  Choose vocoder type of tts task.
+ `--voc_config` VOC_CONFIG Config of voc. Use deault config when it is None.
+ `--voc_ckpt` VOC_CKPT   Checkpoint file of voc.
+ `--voc_stat` VOC_STAT   mean and standard deviation used to normalize spectrogram when training voc.
+ `--lang` LANG           Choose model language. zh or en or mix
+ `--device` DEVICE       Choose device to execute model inference.
+ `--cpu_threads` CPU_THREADS
+ `--output` OUTPUT       output file name
+ `--job_dump_result`, `-d`,  Save job result into file.
+ `--verbose`,`-v`,       Increase logger verbosity of current task.
+ `--use_onnx` USE_ONNX   whether to usen onnxruntime inference.
+ `--fs` FS               sample rate for onnx models when use specified model files.

模型列表

<table style="width:100%">
<thead>
    <tr>
      <th> 语音合成模块类型 </th>
      <th> 模型名称 </th>
      <th> 语言  </th>
      <th> 发音人  </th>
      <th> onnx 支持 </th>
    </tr>
</thead>
<tbody>
    <tr>
        <td rowspan="9">声学模型（am）</td>
        <td>speedyspeech_csmsc</td>
        <td>zh</td>
        <td> 单发音人 </td>
        <td> True </td>
    </tr>
    <tr>
        <td>fastspeech2_csmsc</td>
        <td>zh</td>
        <td> 单发音人 </td>
        <td> True </td>
    </tr>
    <tr>
        <td>fastspeech2_ljspeech</td>
        <td>en</td>
        <td> 单发音人 </td>
        <td> True </td>
    </tr>
    <tr>
        <td>fastspeech2_aishell3</td>
        <td>zh</td>
        <td> 多发音人 0-173 </td>
        <td> True </td>
    </tr>
    <tr>
        <td>fastspeech2_vctk</td>
        <td>en</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>fastspeech2_mix</td>
        <td>mix</td>
        <td> 多发音人 </td>
        <td> True </td>
    </tr>
    <tr>
        <td>tacotron2_csmsc</td>
        <td>zh</td>
        <td> 单发音人 </td>
        <td> False </td>
    </tr>
    <tr>
        <td>tacotron2_ljspeech</td>
        <td>en</td>
        <td> 单发音人 </td>
        <td> False </td>
    </tr>
    <tr>
        <td>fastspeech2_male</td>
        <td>zh</td>
        <td> 单发音人 </td>
        <td> False </td>
    </tr>
    <tr>
        <td rowspan="12">声码器（voc）</td>
        <td>pwgan_csmsc</td>
        <td>zh</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>pwgan_ljspeech</td>
        <td>en</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>pwgan_aishell3</td>
        <td>zh</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>pwgan_vctk</td>
        <td>en</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>mb_melgan_csmsc</td>
        <td>zh</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>style_melgan_csmsc</td>
        <td>zh</td>
        <td> - </td>
        <td> False </td>
    </tr>
    <tr>
        <td>hifigan_csmsc</td>
        <td>zh</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>hifigan_ljspeech</td>
        <td>en</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>hifigan_aishell3</td>
        <td>zh</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>hifigan_vctk</td>
        <td>en</td>
        <td> - </td>
        <td> True </td>
    </tr>
    <tr>
        <td>wavernn_csmsc</td>
        <td>zh</td>
        <td> - </td>
        <td> False </td>
    </tr>
    <tr>
        <td>pwgan_male</td>
        <td>zh</td>
        <td> - </td>
        <td> False </td>
    </tr>
</tbody>
</table>

### Python API

```python
from paddlespeech.cli.tts.infer import TTSExecutor
tts = TTSExecutor()

# 使用默认配置合成
tts(text="今天天气十分不错。", output="output.wav")
```


## 快速服务部署

### 非流式服务部署

### 流式服务部署


## 特色功能

### 小样本语音合成

#### 一句话声音克隆

#### 小样本微调

### 语音语言跨模态大模型文心ERNIE-SAT


## 模型列表

<table style="width:100%">
  <thead>
    <tr>
      <th> 语音合成模块类型 </th>
      <th> 模型类型 </th>
      <th> 数据集  </th>
      <th> 脚本  </th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td> 文本前端</td>
    <td colspan="2"> &emsp; </td>
    <td>
    <a href = "./examples/other/tn">tn</a> / <a href = "./examples/other/g2p">g2p</a>
    </td>
    </tr>
    <tr>
      <td rowspan="5">声学模型</td>
      <td>Tacotron2</td>
      <td>LJSpeech / CSMSC</td>
      <td>
      <a href = "./examples/ljspeech/tts0">tacotron2-ljspeech</a> / <a href = "./examples/csmsc/tts0">tacotron2-csmsc</a>
      </td>
    </tr>
    <tr>
      <td>Transformer TTS</td>
      <td>LJSpeech</td>
      <td>
      <a href = "./examples/ljspeech/tts1">transformer-ljspeech</a>
      </td>
    </tr>
    <tr>
      <td>SpeedySpeech</td>
      <td>CSMSC</td>
      <td >
      <a href = "./examples/csmsc/tts2">speedyspeech-csmsc</a>
      </td>
    </tr>
    <tr>
      <td>FastSpeech2</td>
      <td>LJSpeech / VCTK / CSMSC / AISHELL-3 / ZH_EN / finetune</td>
      <td>
      <a href = "./examples/ljspeech/tts3">fastspeech2-ljspeech</a> / <a href = "./examples/vctk/tts3">fastspeech2-vctk</a> / <a href = "./examples/csmsc/tts3">fastspeech2-csmsc</a> / <a href = "./examples/aishell3/tts3">fastspeech2-aishell3</a> / <a href = "./examples/zh_en_tts/tts3">fastspeech2-zh_en</a> / <a href = "./examples/other/tts_finetune/tts3">fastspeech2-finetune</a>
      </td>
    </tr>
    <tr>
      <td><a href = "https://arxiv.org/abs/2211.03545">ERNIE-SAT</a></td>
      <td>VCTK / AISHELL-3 / ZH_EN</td>
      <td>
      <a href = "./examples/vctk/ernie_sat">ERNIE-SAT-vctk</a> / <a href = "./examples/aishell3/ernie_sat">ERNIE-SAT-aishell3</a> / <a href = "./examples/aishell3_vctk/ernie_sat">ERNIE-SAT-zh_en</a>
      </td>
    </tr>
   <tr>
      <td rowspan="6">声码器</td>
      <td >WaveFlow</td>
      <td >LJSpeech</td>
      <td>
      <a href = "./examples/ljspeech/voc0">waveflow-ljspeech</a>
      </td>
    </tr>
    <tr>
      <td >Parallel WaveGAN</td>
      <td >LJSpeech / VCTK / CSMSC / AISHELL-3</td>
      <td>
      <a href = "./examples/ljspeech/voc1">PWGAN-ljspeech</a> / <a href = "./examples/vctk/voc1">PWGAN-vctk</a> / <a href = "./examples/csmsc/voc1">PWGAN-csmsc</a> /  <a href = "./examples/aishell3/voc1">PWGAN-aishell3</a>
      </td>
    </tr>
    <tr>
      <td >Multi Band MelGAN</td>
      <td >CSMSC</td>
      <td>
      <a href = "./examples/csmsc/voc3">Multi Band MelGAN-csmsc</a> 
      </td>
    </tr>
    <tr>
      <td >Style MelGAN</td>
      <td >CSMSC</td>
      <td>
      <a href = "./examples/csmsc/voc4">Style MelGAN-csmsc</a> 
      </td>
    </tr>
    <tr>
      <td >HiFiGAN</td>
      <td >LJSpeech / VCTK / CSMSC / AISHELL-3</td>
      <td>
      <a href = "./examples/ljspeech/voc5">HiFiGAN-ljspeech</a> / <a href = "./examples/vctk/voc5">HiFiGAN-vctk</a> / <a href = "./examples/csmsc/voc5">HiFiGAN-csmsc</a> / <a href = "./examples/aishell3/voc5">HiFiGAN-aishell3</a>
      </td>
    </tr>
    <tr>
      <td >WaveRNN</td>
      <td >CSMSC</td>
      <td>
      <a href = "./examples/csmsc/voc6">WaveRNN-csmsc</a>
      </td>
    </tr>
    <tr>
      <td rowspan="5">声音克隆</td>
      <td>GE2E</td>
      <td >Librispeech, etc.</td>
      <td>
      <a href = "./examples/other/ge2e">GE2E</a>
      </td>
    </tr>
    <tr>
      <td>SV2TTS (GE2E + Tacotron2)</td>
      <td>AISHELL-3</td>
      <td>
      <a href = "./examples/aishell3/vc0">VC0</a>
      </td>
    </tr>
    <tr>
      <td>SV2TTS (GE2E + FastSpeech2)</td>
      <td>AISHELL-3</td>
      <td>
      <a href = "./examples/aishell3/vc1">VC1</a>
      </td>
    </tr>
    <tr>
      <td>SV2TTS (ECAPA-TDNN + FastSpeech2)</td>
      <td>AISHELL-3</td>
      <td>
      <a href = "./examples/aishell3/vc2">VC2</a>
      </td>
    </tr>
    <tr>
      <td>GE2E + VITS</td>
      <td>AISHELL-3</td>
      <td>
      <a href = "./examples/aishell3/vits-vc">VITS-VC</a>
      </td>
    </tr>
     <tr>
      <td rowspan="3">端到端</td>
      <td>VITS</td>
      <td>CSMSC / AISHELL-3</td>
      <td>
      <a href = "./examples/csmsc/vits">VITS-csmsc</a> / <a href = "./examples/aishell3/vits">VITS-aishell3</a>
      </td>
    </tr>
  </tbody>
</table>

## 飞桨产业特色方案

+ [PP-TTS](./PPTTS_cn.md): 飞桨流式语音合成系统

### 飞桨产业范例

+ [手把手快速搭建智能语音客服——保险问答实践](https://aistudio.baidu.com/aistudio/projectdetail/4497956)
+ [基于PP-TTS的安卓手机部署](https://aistudio.baidu.com/aistudio/projectdetail/5382080)
