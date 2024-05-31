Readers and writers for speech have the `-sp` suffix.

Download the [Iris Living Audio Dataset](https://datasets.cms.waikato.ac.nz/ufdl/living-audio-datasets/) dataset in Festvox format and extract it.

# Plugins

## Festvox to ADAMS

The following converts the Festvoc dataset into ADAMS format, storing the transcript in the `transcript` field:

```bash
adc-convert \
  -l INFO \
  from-festvox-sp \
    -l INFO \
    -i "./festvox/*.txt" \
  to-adams-sp \
    -l INFO \
    -o ./adams \
    -c transcript
```

## Festvox to ADAMS (train/val/test splits)

You can also split the data, e.g., into train, validation and test subsets.
The following converts the Festvox into ADAMS format:

```bash
adc-convert \
  -l INFO \
  from-festvox-sp \
    -l INFO \
    -i "./festvox/*.txt" \
  to-adams-sp \
    -l INFO \
    -o ./adams-split \
    -c transcript \
    --split_names train val test \
    --split_ratios 70 15 15
```

**NB:** The subsets will be placed into sub-directories according to the split name.
