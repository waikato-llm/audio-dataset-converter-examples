The following filters can be used for controlling the execution of the
pipeline:

* `block` - blocks data passing through based on a condition applied to the meta-data
* `list-to-sequence` - forwards the elements of lists individually
* `stop` - stops the pipeline if the meta-data-based condition holds true
* `sub-process` - meta-data condition determines execution of sub-filter(s)
* `tee` - meta-data condition determines forking off of data to the sub-pipeline (filter(s), [writer])
* `trigger` - meta-data condition determines execution of the sub-pipeline (reader, [filter(s)], [writer])


# Sub-pipelines

With the `tee` meta-filter, it is possible to filter the audio files coming through with a separate
sub-pipeline. E.g., converting the incoming data into multiple output formats with their own
preprocessing.

The following command loads the Festvox speech data and saves them in ADAMS and split 
ADAMS format (after trimming silences) in one command:

```bash
adc-convert \
  -l INFO \
  from-festvox-sp \
    -l INFO \
    -i "./festvox/*.txt" \
  tee \
    -f "to-adams-sp -o ./adams-tee/ -t transcript" \
  tee \
    -f "trim-silence to-adams-sp -o ./adams-split-tee/ -t transcript --split_names train val test --split_ratios 70 15 15"
```


# Sub-pipeline file format

`sub-process`, `tee` and `trigger` define their sub-flow either explicitly
as a single command-line or point to a file with the sequence of plugins. The
former should be used for simple sub-flows, whereas the latter makes it easier
to develop more complex ones.

The file format is quite simple:

* plain text with extension of your choice
* line comments start with `#`
* blank lines get ignored
* no line continuation, like `\` or `^`, is required

After stripping the file of blank and comment lines (white spaces at start/end 
of lines get removed as well), all the plugins and their arguments get 
concatenated using spaces. The single command-line is then parsed.

Of course, further sub-pipelines can be defined in such a file. There is no
limit to nesting, as they get expanded/processed as they are encountered.
