# Requirements

Requires the [audio-dataset-converter-redis](https://github.com/waikato-llm/audio-dataset-converter-redis) library.

# Plugins

## Transcribing audio

The following commands loads raw audio files (i.e., ones without a transcript) and
applies the `redis-transcribe` filter to generate a transcript using faster-whisper,
with the result then being stored in Festvox format:

First, start the faster-whisper process via [Docker](https://github.com/waikato-llm/whisper) (using the CPU):

```bash
docker run --rm \
    -u $(id -u):$(id -g) -e USER=$USER \
    --shm-size 8G \
    --net=host \
    -v `pwd`:/workspace \
    -v `pwd`/cache:/.cache \
    -it public.aml-repo.cms.waikato.ac.nz:443/pytorch/python-faster-whisper:1.0.2_cpu \
    fw_predict_redis \
      --redis_in audio \
      --redis_out transcript \
      --model_size base \
      --verbose
```

And now apply the pipeline to have the audio files transcribed:

```bash
adc-convert \
  -l INFO \
    from-data \
      -l INFO \
      -i "./raw/*.wav" \
      -t sp \
    redis-transcribe \
      -l INFO \
      --channel_out audio \
      --channel_in transcript \
    to-festvox-sp \
      -l INFO \
      -o ./festvox
```
