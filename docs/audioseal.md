# Requirements

Requires the [audio-dataset-converter-goruut](https://github.com/waikato-llm/audio-dataset-converter-audioseal) library.

**NB:** Runs quite well on CPU.

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
    -p "wm-audioseal -l INFO -p 42" \
  to-data \
    -l INFO \
    -o ./output/
```

# Watermark detection

The following checks whether the payload `42` is embedded as 16-bit payload 
in the audio (`audioseal-BER` in meta-data should be `0.0` for perfect match 
and `100.0` for no match whatsoever):

```bash
adc-convert -l INFO \
  from-data \
    -l INFO \
    -t sp \
    -i "./output/*.wav" \
  detect-watermark \
    -l INFO \
    -p "wmd-audioseal -l INFO -p 42" \
  get-metadata \
    -f audioseal-BER \
  console
  console \
    -f "df-audio-data -f \"{audio-name}: prob={metadata:audioseal-detect_prob} payload={metadata:audioseal-payload}\""
```
