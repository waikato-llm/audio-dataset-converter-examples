The following sections only show snippets of commands, as there are quite a number of filters available.


## Annotation management

* `strip-annotations` - removes all annotations


## Audio management

* `convert-to-mono` - ensures that audio data is mono
* `convert-to-wav` - ensures that audio data is in WAV format
* `trim-silence` - for removing chunks of silence

Trimming the silence:

```bash
adc-convert -l INFO \
  from-data \
    -l INFO \
    -t sp \
    -i "./input/*.wav" \
  trim-silence \
    -l INFO \
  to-data \
    -l INFO \
    -o ./output
```

## Augmentation

* `pitch-shift` - for shifting the pitch of audio samples
* `time-stretch` - for speeding up/slowing down samples


## Meta-data management

* `metadata` - allows comparisons on meta-data values and whether to keep or discard a record in case of a match
* `metadata-from-name` - allows extraction of meta-data value from the audio file name via a regular expression
* `metadata-to-placeholder` - sets the specified placeholder using the data from the meta-data passing through
* `set-metadata` - sets the meta-data key/value pair as data passes through, can make use of data passing through as well 
* `split-records` - adds a field to the meta-data (default: `split`) of the record passing through, which can be acted on with other filters (or stored in the output)


Splitting records into train/test using a 50/50 split ratio:

```bash
sdc-convert -l INFO -b \
  from-data \
    -l INFO \
    -t sp \
    -i "./input/*.wav" \
  split-records \
    --split_names train test \
    --split_ratios 50 50 \
  set-placeholder
  to-data \
    -l INFO \
    -o ./output
```


## Record management

A number of generic record management filters are available:

* `check-duplicate-filenames` - when using multiple batches as input, duplicate file names can be an issue when creating a combined output
* `discard-by-name` - discards files based on their name, either using explicit names or regular expressions
* `discard-negatives` - removes records from the stream that have no annotations
* `max-records` - limits the number of records passing through
* `randomize-records` - when processing batches, this filter can randomize them (seeded or unseeded)
* `record-window` - only lets a certain window of records pass through (e.g., the first 1000)
* `rename` - allows renaming of audio files, e.g., prefixing them with a batch number/ID
* `sample` - for selecting a random sub-sample from the stream

Discarding files by name:

```bash
adc-convert -l INFO \
  from-subdir-ac \
    -l INFO \
    -i ./input/ \
  discard-by-name \
    -l INFO \
    -r "jvm_00027.*" \
  to-subdir-ac \
    -l INFO \
    -o ./output
```
