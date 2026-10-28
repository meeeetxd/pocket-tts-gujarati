---
language:
- gu
license: cc-by-4.0
pipeline_tag: text-to-speech
base_model: kyutai/pocket-tts
base_model_relation: finetune
inference: false
tags:
- text-to-speech
- voice-cloning
- pocket-tts
- gujarati
---

# Gujarati Pocket TTS

This is a community finetune of [Kyutai Pocket TTS](https://huggingface.co/kyutai/pocket-tts), specifically focused on the Gujarati language. 

It is a 6-layer student distilled from a 24-layer teacher. The tokenizer is SentencePiece. It speaks Gujarati and clones a voice from a short wav. Audio is 24 kHz. The weights are about 438 MB, and CPU is the intended way to run them. Guidance is already baked in, so generate with 1 step and temperature 0.3.

The paper is [Pocket TTS](https://arxiv.org/abs/2509.06926). The base model is [kyutai/pocket-tts](https://huggingface.co/kyutai/pocket-tts), and the code is [kyutai-labs/pocket-tts](https://github.com/kyutai-labs/pocket-tts). The safetensors bundle includes Kyutai's codec weights, used here under CC-BY-4.0.

## Samples

These are generations from this model.

**Gujarati**

જીવન હંમેશા આપણે ધારીએ તે રીતે ચાલતું નથી, પરંતુ ક્યારેક અણધારી ક્ષણો જ સૌથી સુંદર યાદો બની જાય છે.

<audio controls src="https://huggingface.co/meeeetxd/pocket-tts-gujarati/resolve/main/out.wav"></audio>

## Use

Install the library, or call it with `uvx`.

```bash
pip install pocket-tts
```

`weights_path` and `tokenizer_path` in the config are relative. Download this repo and run from that folder:

```python
import scipy.io.wavfile
from pocket_tts import TTSModel

model = TTSModel.load_model(config="config.yaml")
voice = model.get_state_for_audio_prompt("my_voice.wav")
audio = model.generate_audio(voice, "નમસ્તે, તમે કેમ છો?")
scipy.io.wavfile.write("out.wav", model.sample_rate, audio.detach().cpu().numpy().squeeze())
```

The same config on the Hub:

```python
model = TTSModel.load_model(config="hf://meeeetxd/pocket-tts-gujarati/config.yaml")
```

That address loads the yaml. The weight and tokenizer paths inside it stay relative, so `model.safetensors` and `tokenizer.model` still have to sit in the working directory. `config.yaml` and `student.yaml` are the same file.

```bash
uvx pocket-tts generate \
  --config config.yaml \
  --voice my_voice.wav \
  --text "નમસ્તે, તમે કેમ છો?" \
  --output-path out.wav
```

## Model

| | |
| --- | --- |
| Architecture | Pocket TTS flow LM, 6 layers, distilled from 24 |
| Text | SentencePiece tokenizer, Gujarati language focus |
| Sample rate | 24 kHz |
| Decode | 1 step, temperature 0.3 |
| Size | About 438 MB |
| Device | CPU |

Happy to collaborate. If you like this model, give it a like, and follow me for future updates: https://www.linkedin.com/in/meet-patel21"# pocket-tts-gujarati" 
