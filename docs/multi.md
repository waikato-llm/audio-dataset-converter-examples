Most of the time, conversion pipelines will only need to read from one
source and output to a single target. However, there can be cases where
datasets of different types need merging (*multiple inputs*) or datasets
of different types need to generated for different frameworks (*multiple outputs*).

To cater for these scenarios, the following two meta plugins are available:

* `from-multi` - reads from one or more sources using the specified readers
* `to-multi` - forwards the incoming data to one or more writers

There is one restriction, each of the base reader/writer must be from the
same data domain.


# Multiple inputs

The following command reads a dataset in Festvox 
and ADAMS format, with the combined output being saved in CommonVoice format:

```bash
adc-convert \
  -l INFO \
  from-multi \
    -l INFO \
    -t sp \
    -r "from-festvox-sp -l INFO -i {CWD}/input/*.txt" \
       "from-adams-sp -l INFO -i {CWD}/input/*.report -t transcript" \
  to-commonvoice-sp \
    -l INFO \
    -o "{CWD}/output"
```

# Multiple outputs

Below, the source data is in ADAMS speech format and will be
converted to Festvox and CommonVoice format:

```bash
adc-convert \
  -l INFO \
  from-adams-sp \
    -l INFO \
    -i "{CWD}/input/*.report" \
  to-multi \
    -l INFO \
    -t sp \
    -w "to-festvox-sp -l INFO -o {CWD}/output/festvox" \
       "to-commonvoice-sp -l INFO -o {CWD}/output/commonvoice"
```
