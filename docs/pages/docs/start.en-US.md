
## 🚀 One-Click Integrated Package for Windows

### Important Notes:

1. The integrated package uses the CPU version of torch, with a size of about **2.5G**.
2. When using UVR5 for noise reduction in the dubbing step, the CPU version will be significantly slower than GPU-accelerated torch.
3. The integrated package **only supports calling whisperX ☁️ via API**, and does not support running whisperX locally 💻.

If you need the following features, please install from source code (requires an Nvidia GPU and at least **20G** of disk space):
- Run whisperX locally 💻
- Use GPU-accelerated UVR5 for noise reduction

### Download and Usage Instructions

1. Download the `v1.2.0` one-click package (750M): [Download Directly](https://vip.123pan.cn/1817874751/8158115) | [Baidu Backup](https://pan.baidu.com/s/1H_3PthZ3R3NsjS0vrymimg?pwd=ra64)

2. After extracting, double-click `OneKeyStart.bat` in the folder

3. In the opened browser window, configure the necessary settings in the sidebar, then create your video with one click!
  ![settings](https://github.com/user-attachments/assets/3d99cf63-ab89-404c-ae61-5a8a3b27d840)

> 💡 Note: This project requires configuration of large language models, WhisperX, and TTS. Please carefully read the **API Preparation** section below

## 📋 API Preparation
This project requires the use of large language models, WhisperX, and TTS. Multiple options are provided for each component. **Please read the configuration guide carefully 😊**
### 1. **Obtain API_KEY for Large Language Models**:

| Recommended Model | Recommended Provider | base_url | Price | Effect |
|:-----|:---------|:---------|:-----|:---------|
| claude-3-5-sonnet-20240620 (default) | [Yunwu API](https://yunwu.zeabur.app/register?aff=TXMB) | https://yunwu.zeabur.app | ¥15 / 1M tokens | 🤩 |
| deepseek-coder | [deepseek](https://platform.deepseek.com/api_keys) | https://api.deepseek.com | ¥2 / 1M tokens | 😲 |
> Note: Yunwu API also supports OpenAI's tts-1 interface, which can be used in the dubbing step.

> Reminder: deepseek has a very low probability of errors during translation, if errors occur, please switch to sonnet...

#### Common Questions

<details>
<summary>How to choose a model?</summary>

- 🌟 Default use of Claude 3.5, excellent translation quality, very good coherence, no AI flavor.
- 🚀 If using deepseek, translating a 1-hour video costs about ¥1, with average results.
</details>

<details>
<summary>How to get an API key?</summary>

1. Click the link for the recommended provider above
2. Register an account and recharge
3. Create a new API key on the API key page
4. For Yunwu API, make sure to check `Unlimited Quota`, select the `claude-3-5-sonnet-20240620` model, and it is recommended to choose the `Pure AZ 1.5x` channel.
</details>

<details>
<summary>Can I use other models?</summary>

- ✅ Supports OAI-Like API interfaces, but you need to change it yourself in the Streamlit sidebar.
- ⚠️ However, other models (especially small models) have weak ability to follow instructions and are very likely to report errors during translation, which is strongly discouraged.
</details>

### 2. **Prepare Replicate Token** (Only when using whisperXapi ☁️)

VideoLingo uses WhisperX for speech recognition, supporting both local deployment and cloud API.
#### Comparison of options:
| Option | Disadvantages |
|:-----|:-----|
| **whisperX 🖥️** | • Install CUDA 🛠️<br/>• Download model 📥<br/>• High VRAM requirement 💾 |
| **whisperXapi ☁️ (Recommended)** | • Requires VPN 🕵️‍♂️<br/>• Visa card 💳 |

#### Obtaining the token
   - Register at [Replicate](https://replicate.com/account/api-tokens), bind a Visa card payment method, and obtain the token
   - **Or join the QQ group to get a free test token from the group announcement**

### 3. **TTS API**
VideoLingo provides multiple TTS integration methods. Here's a comparison (skip this if you're only translating without dubbing):

| TTS Option | Advantages | Disadvantages | Chinese Effect | Non-Chinese Effect |
|:---------|:-----|:-----|:---------|:-----------|
| 🎙️ OpenAI TTS | High quality, realistic emotion | Chinese sounds like a foreigner | 😕 | 🤩 |
| 🔊 Azure TTS  | Natural effect | Inconvenient recharge | 🤩 | 😃 |
| 🎤 Fish TTS (Recommended) | Excellent | Requires recharge | 😱 | 😱 |
| 🗣️ GPT-SoVITS (beta) | Local, cloning | Currently only supports English input Chinese output, requires GPU for model training, best for single-person videos without obvious BGM, and the base model should be close to the original voice | 😂 | 🚫 |

For OpenAI TTS, we recommend using [Yunwu API](https://yunwu.zeabur.app/register?aff=TXMB); **Azure TTS free keys can be obtained in the QQ group** or you can register and recharge yourself on the [official website](https://learn.microsoft.com/zh-cn/azure/ai-services/speech-service/get-started-text-to-speech?tabs=windows%2Cterminal&pivots=programming-language-python); **Fish TTS free keys can be obtained in the QQ group** or you can register and recharge yourself on the [official website](https://fish.audio/zh-CN/go-api/).

<details>
<summary>How to choose an Azure voice?</summary>

It is recommended to listen and choose the voice you want in the [online experience](https://speech.microsoft.com/portal/voicegallery), and find the corresponding code for that voice in the right-hand code, such as `zh-CN-XiaoxiaoMultilingualNeural`.

</details>

<details>
<summary>How to choose a Fish TTS voice?</summary>

Go to the [official website](https://fish.audio/zh-CN/) to listen and choose the voice you want, and find the corresponding code for that voice in the URL, such as Ding Zhen is `54a5170264694bfc8e9ad98df7bd89c3`. Popular voices have been added to `config.py`, just modify `FISH_TTS_CHARACTER`. If you need to use other voices, please modify the `FISH_TTS_CHARACTER_ID_DICT` dictionary in `config.py`.

</details>

<details>
<summary>GPT-SoVITS-v2 Usage Tutorial</summary>

1. Go to the [official Yuque document](https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e/dkxgpiy9zb96hob4#KTvnO) to check the configuration requirements and download the integrated package.

2. Place `GPT-SoVITS-v2-xxx` in the same directory level as `VideoLingo`. **Note that they should be parallel, not nested.**

3. Choose one of the following methods to configure the model:

   a. Self-trained model:
   - After training the model, `tts_infer.yaml` under `GPT-SoVITS-v2-xxx\GPT_SoVITS\configs` will automatically be filled with your model address. Copy and rename it to `your_preferred_character_name.yaml`
   - In the same directory as the `yaml` file, place the reference audio you'll use later, named `your_preferred_character_name_text_content_of_reference_audio.wav` or `.mp3`, for example `Huanyuv2_Hello, this is a test audio.wav`
   - In the sidebar of the VideoLingo webpage, set `GPT-SoVITS Character` to `your_preferred_character_name`.

   b. Use pre-trained model:
   - Download my model from [here](https://vip.123pan.cn/1817874751/8137723), extract and overwrite to `GPT-SoVITS-v2-xxx`.
   - Set `GPT-SoVITS Character` to `Huanyuv2`.

   c. Use other trained models:
   - Place model files in `GPT_weights_v2` and `SoVITS_weights_v2` respectively.
   - Refer to method a, rename and modify the paths in `tts_infer.yaml` to point to your two models.
   - Refer to method a, place the reference audio you'll use later in the same directory as the `yaml` file, named `your_preferred_character_name_text_content_of_reference_audio.wav` or `.mp3`

   ```
   # Directory structure example
   .
   ├── VideoLingo
   │   └── ...
   └── GPT-SoVITS-v2-xxx
       ├── GPT_SoVITS
       │   └── configs
       │       ├── tts_infer.yaml
       │       ├── your_preferred_character_name.yaml
       │       └── your_preferred_character_name_text_content_of_reference_audio.wav
       ├── GPT_weights_v2
       │   └── [Your GPT model file]
       └── SoVITS_weights_v2
           └── [Your SoVITS model file]
   ```
        
After configuration, VideoLingo will automatically open the inference API port of GPT-SoVITS in the pop-up command line during the dubbing step. You can manually close it after dubbing is complete. Note that this method is still not very stable and may result in missing words or sentences, so please use it with caution.</details>

## 🛠️ Source Code Installation Process

### Windows Prerequisites

Before starting the installation of VideoLingo, please ensure you have **20G** of free disk space and complete the following steps:

| Dependency | whisperX 🖥️ | whisperX ☁️ |
|:-----|:-------------------|:----------------|
| Anaconda 🐍 | [Download](https://www.anaconda.com/products/distribution#download-section) | [Download](https://www.anaconda.com/products/distribution#download-section) |
| Git 🌿 | [Download](https://git-scm.com/download/win) | [Download](https://git-scm.com/download/win) |
| Cuda Toolkit 12.6 🚀 | [Download](https://developer.download.nvidia.com/compute/cuda/12.6.0/local_installers/cuda_12.6.0_560.76_windows.exe) | - |
| Cudnn 9.3.0 🧠 | [Download](https://developer.download.nvidia.com/compute/cudnn/9.3.0/local_installers/cudnn_9.3.0_windows.exe) | - |

> Note: When installing Anaconda, check "Add to system Path", and restart your computer after installation 🔄

### Installation Steps

Supports Win, Mac, Linux. If you encounter any issues, you can ask GPT about the entire process~
1. Open Anaconda Powershell Prompt and switch to the desktop directory:
   ```bash
   cd desktop
   ```

2. Clone the project:
   ```bash
   git clone https://github.com/Huanshere/VideoLingo.git
   cd VideoLingo
   ```

3. Configure virtual environment (must be 3.10.0):
   ```bash
   conda create -n videolingo python=3.10.0 -y
   conda activate videolingo
   ```

4. Run the installation script:
   ```bash
   python install.py
   ```
   Follow the prompts to select the desired Whisper project, the script will automatically install the corresponding torch and whisper versions

   Note: Mac users need to manually install ffmpeg according to the prompts

5. 🎉 Enter the command or click `OneKeyStart.bat` to launch the Streamlit application:
   ```bash
   streamlit run st.py
   ```

6. Set the key in the sidebar of the pop-up webpage, and be sure to select the whisper method

   ![settings](https://github.com/user-attachments/assets/3d99cf63-ab89-404c-ae61-5a8a3b27d840)

This project uses structured module development. You can run `core\step__.py` files in sequence. Technical documentation: [Chinese](./docs/README_guide_zh.md) | [English](./docs/README_guide_en.md) (To be updated)
