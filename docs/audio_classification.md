Readers and writers for audio classification have the `-ac` suffix.

# Plugins

## sub-dir to ADAMS

The following converts an audio classification dataset from the sub-dir format
(sub-directory names represent the audio classification labels) into the 
[ADAMS format](https://github.com/waikato-llm/audio-dataset-converter/blob/main/formats/adams.md), 
which stores the label in an associated .report file (Java properties file):

```bash
adc-convert -l INFO \
  from-subdir-ac \
    -l INFO \
    -i ./subdir/ \
  to-adams-ac \
    -l INFO \
    -o ./adams \
    -c classification
```


## sub-dir (randomized train/val/test splits)

By enforcing batch-processing `--force_batch` and using the 
`randomize-records` filter, randomized train/val/test splits
(writers typically support generating splits) can be generated 
like this:

```bash
adc-convert -l INFO --force_batch \
  from-subdir-ac \
    -l INFO \
    -i ./subdir/ \
  randomize-records \
    -s 42 \
  to-subdir-ac \
    -l INFO \
    -o ./subdir-split \
    -c classification \
    --split_names train val test \
    --split_ratios 70 15 15
```
