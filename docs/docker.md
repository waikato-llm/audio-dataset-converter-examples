Below are examples for using the audio-dataset-converter library via its 
[Docker images](https://github.com/waikato-datamining/audio-dataset-converter-all/tree/main/docker).


# Interactive session

The following command starts an interactive session, mapping the current working
directory to `/workspace`:

```bash
docker run --rm -u $(id -u):$(id -g) \
    -v `pwd`:/workspace \
    -it waikatodatamining/audio-dataset-converter:latest
```

# Conversion pipeline

The following converts an audio classification dataset from the sub-dir format
(sub-directory names represent the audio classification labels) into the 
[ADAMS format](https://github.com/waikato-datamining/audio-dataset-converter/blob/main/formats/adams.md), 
which stores the label in an associated .report file (Java properties file):

```bash
docker run --rm -u $(id -u):$(id -g) \
    -v `pwd`:/workspace \
    -it waikatodatamining/audio-dataset-converter:latest \
    adc-convert -l INFO \
      from-subdir-ac \
        -l INFO \
        -i /workspace/input/ \
      to-adams-ac \
        -l INFO \
        -o /workspace/output \
        -c classification
```

**NB:** The `input` and `output` directories are located below the current working directory (`pwd`).
