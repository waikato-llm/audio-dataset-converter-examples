# Requirements

Requires the [audio-dataset-converter-phonemizer](https://github.com/waikato-llm/audio-dataset-converter-phonemizer) library.

# espeak

The following command loads Norwegian speech data in common-voice format, 
phonemizes it using the `ph-espeak` plugin and stores it in Piper output format:

```bash
adc-convert \
  -l INFO \
  from-commonvoice-sp \
    -l INFO \
    -i "./input/train.tsv" \
    --rel_path clips \
  phonemize \
    -l INFO \
    -p "ph-espeak -L nb" \
  convert-to-wav \
  to-piper-sp \
    -l INFO \
    -o ./output
```
