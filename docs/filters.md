The following sections only show snippets of commands, as there are quite a number of filters available.


## Annotation management

* `strip-annotations` - removes all annotations


## Audio management

* `to-mono` - ensures that audio data is mono


## Meta-data management

* `metadata` - allows comparisons on meta-data values and whether to keep or discard a record in case of a match
* `metadata-from-name` - allows extraction of meta-data value from the audio file name via a regular expression
* `split` - adds the field `split` to the meta-data of the record passing through, which can be acted on with other filters (or stored in the output)


## Record management

A number of generic record management filters are available:

* `check-duplicate-filenames` - when using multiple batches as input, duplicate file names can be an issue when creating a combined output
* `discard-negatives` - removes records from the stream that have no annotations
* `max-records` - limits the number of records passing through
* `randomize-records` - when processing batches, this filter can randomize them (seeded or unseeded)
* `record-window` - only lets a certain window of records pass through (e.g., the first 1000)
* `rename` - allows renaming of audio files, e.g., prefixing them with a batch number/ID
* `sample` - for selecting a random sub-sample from the stream


## Sub-pipelines

With the `tee` meta-filter, it is possible to filter the audio files coming through with a separate
sub-pipeline. E.g., converting the incoming data into multiple output formats.

The following command loads the Festvox speech data and saves them in ADAMS and split ADAMS format in one command:

```bash
adc-convert \
  -l INFO \
  from-festvox-sp \
    -l INFO \
    -i "./festvox/*.txt" \
  tee \
    -f "to-adams-sp -o ./adams-tee/ -c transcript" \
  tee \
    -f "to-adams-sp -o ./adams-split-tee/ -c transcript --split_names train val test --split_ratios 70 15 15"
```
