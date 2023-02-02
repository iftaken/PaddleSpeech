# PaddleSpeech 语音识别

PaddleSpeech 语音识别主页，快速帮助你上手 PaddleSpeech 语音识别能力.

### 效果展示

##### 语音识别

<div align = "center">
<table style="width:100%">
  <thead>
    <tr>
      <th> 输入音频  </th>
      <th width="550"> 识别结果 </th>
    </tr>
  </thead>
  <tbody>
   <tr>
      <td align = "center">
      <a href="https://paddlespeech.bj.bcebos.com/PaddleAudio/en.wav" rel="nofollow">
            <img align="center" src="./docs/images/audio_icon.png" width="200 style="max-width: 100%;"></a><br>
      </td>
      <td >I knocked at the door on the ancient side of the building.</td>
    </tr>
    <tr>
      <td align = "center">
      <a href="https://paddlespeech.bj.bcebos.com/PaddleAudio/zh.wav" rel="nofollow">
            <img align="center" src="./docs/images/audio_icon.png" width="200" style="max-width: 100%;"></a><br>
      </td>
      <td>我认为跑步最重要的就是给我带来了身体健康。</td>
    </tr>
  </tbody>
</table>

</div>

## 安装

PaddleSpeech 安装请参考 主页 Readme 中[【安装】](https://github.com/PaddlePaddle/PaddleSpeech/blob/develop/README_cn.md#%E5%AE%89%E8%A3%85)部分，请确保 PaddleSpeech 安装完整。



## 快速开始

测试音频示例下载

```bash
# 中文示例音频
wget -c https://paddlespeech.bj.bcebos.com/PaddleAudio/zh.wav
# 英文示例音频
wget -c https://paddlespeech.bj.bcebos.com/PaddleAudio/en.wav
# 中英混合示例音频
wget -c https://paddlespeech.bj.bcebos.com/PaddleAudio/ch_zh_mix.wav
```

### 命令行

PaddleSpeech 语音识别功能支持通过命令行快速使用体验，支持多种语音识别模型。

通过默认项快速启动，第一次使用时自动下载内置预训练模型，默认预训练模型有时会随版本迭代更新，如果需要固定模型类型，请指定`--model`参数。默认情况下只支持`16k 16bit`的`wav`文件，其它采样率可以通过`--yes`参数进行强制重采样，如果是`mp3`或`ogg`等其它格式，使用前 可以通过`--help`了解`CLI`中支持的参数以及支持的模型列表

快速体验示例：
```bash
# 注意事项：默认音频示例使用的是采样率16k，存储位数为16bit的wav文件
# 识别中文音频
paddlespeech asr --input zh.wav
# 识别英文音频
paddlespeech asr --model transformer_librispeech --lang en --input ./en.wav
# 识别中英混合识别音频
paddlespeech asr --model conformer_talcs --lang zh_en --codeswitch True --input ./ch_zh_mix.wav
# 中文语音识别 + 标点回复
paddlespeech asr --input ./zh.wav -v | paddlespeech text --task punc -v
# 识别中文音频（非16k，会强制进行重采样）
paddlespeech asr --lang zh --input zh.wav --yes
# 指定语音识别模型，模型列表见 -h 参数列表
paddlespeech asr --model conformer_wenetspeech --lang zh --input zh.wav
```

`--help` 参数，获取参数说明列表（包含支持的模型列表）

```bash
paddlespeech asr --help
```

部分参数说明：

+ `--help`, `-h` : 帮助说明
+ `--input` (必须输入): 用于识别的音频文件
+ `--model` : ASR 任务模型，默认值：conformer_u2pp_online_wenetspeech
+ `--lang` : 选择模型语言，默认中文 [zh, en, zh_en], Default: zh.
+ `--codeswitch` : 选择是否开启code-switch，目前只支持`conformer_talcs`模型，适用于中英混合语音识别 `True` or `False` 布尔类型.
+ `--config` : ASR 识别任务配置文件，默认为None，选择预训练模型中的配置文件
+ `--decode_method` : 解码方式，只支持 transformer 和 conformer模型，可选[ctc_greedy_search,ctc_prefix_beam_search,attention,attention_rescoring]
+ `--num_decoding_left_chunks`, `-num_left`: 只支持 transformer 和conformer 的 online 模型
+ `--ckpt_path` : 模型 checkpoint 路径，默认为None，自动下载预训练模型
+ `--yes`, `-y` : 将输入的音频强制重采样到16k
+ `--device` : 选择模型推理硬件
+ `--job_dump_result`, `-d`: 将识别结果保存到文件
+ `--verbose`, `-v` : 提高当前任务的日志等级


`--model` 支持模型列表说明：
|模型名称|模型结构|数据集|类型|支持语言|采样率| codeswitch | decode_method | num_decoding_left_chunks |
|-|-|-|-|-|-|-|-|-|
| conformer_wenetspeech | conformer | wenetspeech | offline | zh | 16k | - | - | - |
| conformer_online_wenetspeech | conformer | wenetspeech | online | zh | 16k | - | - | - | 
| conformer_u2pp_online_wenetspeech | conformer_u2pp | wenetspeech | online | zh | 16k | - | - | - | 
| conformer_online_multicn | conformer | multicn | online | zh | 16k | - | - | - |
| conformer_aishell | conformer | aishell | offline | zh | 16k | - | - | - |
| conformer_online_aishell | conformer | aishell | online | zh | 16k | - | - | - |
| transformer_librispeech | transformer | librispeech | offline | en | 16k | - | - | - |
| deepspeech2online_wenetspeech | deepspeech2 | wenetspeech | online | zh | 16k | - | - | - |
| deepspeech2offline_aishell | deepspeech2 | aishell | offline | zh | 16k | - | - | - |
| deepspeech2online_aishell | deepspeech2 | aishell | online | zh | 16k | - | - | - |
| deepspeech2offline_librispeech | deepspeech2 | librispeech | offline | en | 16k | - | - | - |
| conformer_talcs | conformer | talcs | offline | zh_en | 16k | True | - | - |



### Python API

PaddleSpeech 语音识别功能同样支持 `Python` 调用， 源代码可以参考 [`infer.py`](paddlespeech/cli/asr/infer.py)

```python
import paddle
from paddlespeech.cli.asr import ASRExecutor

asr_executor = ASRExecutor()
text = asr_executor(
    model='conformer_wenetspeech',
    lang='zh',
    sample_rate=16000,
    config=None,  # Set `config` and `ckpt_path` to None to use pretrained model.
    ckpt_path=None,
    audio_file='./zh.wav',
    force_yes=False,
    device=paddle.get_device())
print('ASR Result: \n{}'.format(text))
```

`ASRExecutor` 的参数也可以参考上面的模型列表说明

## 快速服务部署

通过 `PaddleSpeech` 的 `paddlespeech_server` 服务可以快速开启语音识别服务，支持非流式语音识别与流式语音识别。有关 `Speech Server` 更多内容可以参考[Speech Server 语音服务文档](../../../demos/speech_server/README_cn.md)

服务接口定义请参考:
+ [PaddleSpeech Server RESTful API](https://github.com/PaddlePaddle/PaddleSpeech/wiki/PaddleSpeech-Server-RESTful-API)

### 非流式语音识别

#### 服务端

```bash
paddlespeech_server start --config_file ./demos/speech_server/conf/application.yaml
```

#### 客户端

```bash
paddlespeech_client asr --server_ip 127.0.0.1 --port 8090 --input input_16k.wav
```

### 流式语音识别

更多内容，可以参考[流式语音识别服务文档](../../../demos/streaming_asr_server/README_cn.md)

#### 服务端

```bash
paddlespeech_server start --config_file ./demos/streaming_asr_server/conf/application.yaml
```

#### 客户端

```bash
paddlespeech_client asr_online --server_ip 127.0.0.1 --port 8090 --input input_16k.wav
```

你可以通过 `paddlespeech_client` 中流式语音识别客户端的示例，在需要使用流式语音识别的场景中，构建自己的流式语音识别客户端。

## whisper

Whisper是一种通用的语音识别模型。它是在多种音频的大数据集上训练的，也是一个多任务模型，可以执行多语言语音识别以及语音翻译和语言识别。

更多内容可以参考[whisper说明文档](../../../demos/whisper/README_cn.md)

### 使用方法

#### 命令行
```bash
# 识别文本
paddlespeech whisper --task transcribe --input ./zh.wav

#选择只支持英文的模型，并且更换不同大小的模型
paddlespeech whisper --lang en --size base --task transcribe  --input ./en.wav

# 将语音翻译成英语
paddlespeech whisper --task translate --input ./zh.wav
```

使用方法：

```bash
paddlespeech whisper --help
```

#### Python API

```python
import paddle
from paddlespeech.cli.whisper import WhisperExecutor

whisper_executor = WhisperExecutor()

# 识别文本
text = whisper_executor(
    model='whisper',
    task='transcribe',
    sample_rate=16000,
    config=None,  # Set `config` and `ckpt_path` to None to use pretrained model.
    ckpt_path=None,
    audio_file='./zh.wav',
    device=paddle.get_device())
print('ASR Result: \n{}'.format(text))

 # 将语音翻译成英语
feature = whisper_executor(
    model='whisper',
    task='translate',
    sample_rate=16000,
    config=None,  # Set `config` and `ckpt_path` to None to use pretrained model.
    ckpt_path=None,
    audio_file='./zh.wav',
    device=paddle.get_device())
print('Representation: \n{}'.format(feature))
```

## 模型列表

PaddleSpeech 支持多种语音识别相关的模型，对应的数据集和训练脚本如下，更详细的预训练模型信息，详细可以见[模型列表](./docs/source/released_model.md)

<table style="width:100%">
  <thead>
    <tr>
      <th>语音转文本模块类型</th>
      <th>数据集</th>
      <th>模型类型</th>
      <th>脚本</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">语音识别</td>
      <td rowspan="2" >Aishell</td>
      <td >DeepSpeech2 RNN + Conv based Models</td>
      <td>
      <a href = "./examples/aishell/asr0">deepspeech2-aishell</a>
      </td>
    </tr>
    <tr>
      <td>Transformer based Attention Models </td>
      <td>
      <a href = "./examples/aishell/asr1">u2.transformer.conformer-aishell</a>
      </td>
    </tr>
      <tr>
      <td> Librispeech</td>
      <td>Transformer based Attention Models </td>
      <td>
      <a href = "./examples/librispeech/asr0">deepspeech2-librispeech</a> / <a href = "./examples/librispeech/asr1">transformer.conformer.u2-librispeech</a>  / <a href = "./examples/librispeech/asr2">transformer.conformer.u2-kaldi-librispeech</a>
      </td>
      </td>
    </tr>
    <tr>
      <td>TIMIT</td>
      <td>Unified Streaming & Non-streaming Two-pass</td>
      <td>
    <a href = "./examples/timit/asr1"> u2-timit</a>
      </td>
    </tr>
   <tr>
      <td rowspan="1">语言模型</td>
      <td colspan = "2">Ngram 语言模型</td>
      <td>
      <a href = "./examples/other/ngram_lm">kenlm</a>
      </td>
    </tr>
  </tbody>
</table>


## 飞桨产业特色方案

+ [PP-ASR](./PPASR_cn.md)：超轻量高精度流式语音识别系统


### 飞桨产业范例

+ [基于 PP-ASR 的长语音识别](https://aistudio.baidu.com/aistudio/projectdetail/5164530)
+ [智能语音指令解析系统全流程搭建，实现语音工单信息抽取](https://aistudio.baidu.com/aistudio/projectdetail/4398167)
+ [手把手快速搭建智能语音客服——保险问答实践](https://aistudio.baidu.com/aistudio/projectdetail/4497956)
