The following sections only show snippets of commands, as there are quite a number of filters available.


## Annotation management

* `strip-annotations` - removes all annotations


## Audio management

* `convert-to-mono` - ensures that audio data is mono
* `convert-to-wav` - ensures that audio data is in WAV format
* `trim-silence` - for removing chunks of silence


## Augmentation

* `pitch-shift` - for shifting the pitch of audio samples
* `time-stretch` - for speeding up/slowing down samples


## Meta-data management

* `metadata` - allows comparisons on meta-data values and whether to keep or discard a record in case of a match
* `metadata-from-name` - allows extraction of meta-data value from the audio file name via a regular expression
* `split-records` - adds the field `split` to the meta-data of the record passing through, which can be acted on with other filters (or stored in the output)


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
