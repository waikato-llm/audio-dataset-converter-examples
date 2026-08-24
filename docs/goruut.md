# Requirements

Requires the [audio-dataset-converter-goruut](https://github.com/waikato-llm/audio-dataset-converter-goruut) library.

# Phonemization

The following command loads Norwegian speech data in common-voice format, 
phonemizes it using the `ph-goruut` plugin and stores it in Piper output format:

```bash
adc-convert \
  -l INFO \
  from-commonvoice-sp \
    -l INFO \
    -i "./input/train.tsv" \
    --rel_path clips \
  phonemize \
    -l INFO \
    -p "ph-goruut -L Norwegian" \
  convert-to-wav \
  to-piper-sp \
    -l INFO \
    -o ./output
```
