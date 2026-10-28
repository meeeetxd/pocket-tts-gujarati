# Gujarati Pocket TTS

[![Hugging Face Model](https://img.shields.io/badge/🤗%20Hugging%20Face-Model-blue)](https://huggingface.co/meeeetxd/pocket-tts-gujarati)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

This is a community finetune of [Kyutai Pocket TTS](https://github.com/kyutai-labs/pocket-tts), specifically focused on the Gujarati language. 

It is a 6-layer student distilled from a 24-layer teacher. The tokenizer is SentencePiece. It speaks Gujarati and clones a voice from a short `.wav` file. Audio is generated at 24 kHz. The model weights are lightweight (about 438 MB) and are intended to run efficiently on a CPU. Guidance is already baked in, so you can generate high-quality audio with just 1 step and a temperature of 0.3.

## 🎧 Samples

These are generations produced directly by this finetuned model.

**Gujarati**

> જીવન હંમેશા આપણે ધારીએ તે રીતે ચાલતું નથી, પરંતુ ક્યારેક અણધારી ક્ષણો જ સૌથી સુંદર યાદો બની જાય છે.

<audio controls src="https://huggingface.co/meeeetxd/pocket-tts-gujarati/resolve/main/out.wav"></audio>

*(Note: If the audio player doesn't render in your markdown viewer, you can listen to the sample directly [here](https://huggingface.co/meeeetxd/pocket-tts-gujarati/resolve/main/out.wav)).*

## 🚀 Installation & Usage

Install the library via pip, or call it directly with `uvx`.

```bash
pip install pocket-tts
```

### Running Locally

`weights_path` and `tokenizer_path` in the config are relative. Clone this repository, navigate to the folder, and run:

```python
import scipy.io.wavfile
from pocket_tts import TTSModel

model = TTSModel.load_model(config="config.yaml")
voice = model.get_state_for_audio_prompt("my_voice.wav")
audio = model.generate_audio(voice, "નમસ્તે, તમે કેમ છો?")
scipy.io.wavfile.write("out.wav", model.sample_rate, audio.detach().cpu().numpy().squeeze())
```

### Running from Hugging Face Hub

You can also load the configuration directly from the Hub:

```python
from pocket_tts import TTSModel

model = TTSModel.load_model(config="hf://meeeetxd/pocket-tts-gujarati/config.yaml")
```

*Note: Loading from the Hub fetches the `yaml` file. The weight and tokenizer paths inside it stay relative, meaning `model.safetensors` and `tokenizer.model` still need to be in your local working directory. (`config.yaml` and `student.yaml` are the same file).*

### CLI Usage (via uvx)

```bash
uvx pocket-tts generate \
  --config config.yaml \
  --voice my_voice.wav \
  --text "નમસ્તે, તમે કેમ છો?" \
  --output-path out.wav
```

## 📊 Model Specifications

| Feature | Details |
| :--- | :--- |
| **Architecture** | Pocket TTS flow LM, 6 layers, distilled from 24 |
| **Text** | SentencePiece tokenizer, Gujarati language focus |
| **Sample rate** | 24 kHz |
| **Decode** | 1 step, temperature 0.3 |
| **Size** | ~ 438 MB |
| **Hardware** | CPU-friendly |

## 📚 Acknowledgments & References

* **Paper:** [Pocket TTS](https://arxiv.org/abs/2509.06926)
* **Base Model:** [kyutai/pocket-tts](https://huggingface.co/kyutai/pocket-tts)
* **Original Codebase:** [kyutai-labs/pocket-tts](https://github.com/kyutai-labs/pocket-tts)
* The safetensors bundle includes Kyutai's codec weights, used here under CC-BY-4.0.

## 🤝 Let's Collaborate

Happy to collaborate on future open-source AI projects. If you like this model, please consider giving the repository a ⭐! 

Feel free to connect and follow me for future updates:  
🔗 **[LinkedIn - Meet Patel](https://www.linkedin.com/in/meet-patel21)**