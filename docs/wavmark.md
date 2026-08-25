# Requirements

Requires the [audio-dataset-converter-goruut](https://github.com/waikato-llm/audio-dataset-converter-wavmark) library.

**NB:** A GPU device is recommended to speed up processing.

# Watermarking

The following embeds the payload `42` as 16-bit payload in the audio:

```bash
adc-convert -l INFO \
  from-data \
    -l INFO \
    -t sp \
    -i "./input/*.wav" \
  embed-watermark \
    -l INFO \
    -p "wm-wavmark -l INFO -p 42" \
  to-data \
    -l INFO \
    -o ./output/
```

# Watermark detection

The following checks whether the payload `42` is embedded as 16-bit payload 
in the audio (`wavmark-BER` in meta-data should be `0.0`):

```bash
adc-convert -l INFO \
  from-data \
    -l INFO \
    -t sp \
    -i "./output/*.wav" \
  detect-watermark \
    -l INFO \
    -p "wmd-wavmark -l INFO -p 42" \
  get-metadata \
    -f wavmark-BER \
  console
```
