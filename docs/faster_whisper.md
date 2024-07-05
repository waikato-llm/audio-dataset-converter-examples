# Requirements

Requires the [audio-dataset-converter-faster-whisper](https://github.com/waikato-llm/audio-dataset-converter-faster-whisper) library.

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


# Tools

## Generate SRT subtitles

The `adc-srt` allows generating subtitles in [SRT format](https://docs.fileformat.com/video/srt/) from audio
and video files.

The following example generates subtitle files for all `.mp4` file, alongside the video files:

```bash
adc-srt \
  -l INFO \
  -i ./input/*.mp4
```

In this example, the `.srt` files generated from `.wav` files get placed in a separate output directory:

```bash
adc-srt \
  -l INFO \
  -i ./input/*.wav \
  -o ./output
```
