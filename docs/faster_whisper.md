# Requirements

Requires the [audio-dataset-converter-faster-whisper](https://github.com/waikato-datamining/audio-dataset-converter-faster-whisper) library.

# Plugins

## Transcribing audio

The following commands loads raw audio files (i.e., ones without a transcript) and
applies the `fw-transcribe` filter to generate a transcript using faster-whisper,
with the result then being stored in Festvox format:

```bash
adc-convert \
  -l INFO \
    from-data \
      -l INFO \
      -i "./raw/*.wav" \
      -t sp \
    fw-transcribe \
      -l INFO \
    to-festvox-sp \
      -l INFO \
      -o ./festvox
```
