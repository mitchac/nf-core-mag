Install unzip
```
sudo apt install unzip
```
Install ampliseq
```
wget https://github.com/nf-core/ampliseq/archive/master.zip
```
Unzip documents
```
mkdir -p ~/my-pipelines/nf-core/
```
```
unzip master.zip -d ~/my-pipelines/nf-core/
```
Install docker
```
sudo apt install docker.io
```
```
sudo usermod -aG docker ubuntu
```
```
Exit
```

*Edit analysis pipeline config files*

Configure required system variables for analysis pipeline

```
export TMPDIR=/data/tmp
export NXF_TEMP=/data/tmp
export NXF_WORK=/data/work
export PATH=/home/ubuntu:$PATH
```

Running analysis pipeline

```
nextflow run main.nf \
    -profile conda \
    --reads "/path/to/folder" \
    --FW_primer AGGATTAGATACCCTGGTA \
    --RV_primer CRRCACGAGCTGACGAC \
    --metadata "/path/to/data/sample_*_{1,2}.fastq or tsv" \
    --reference_database Silva_132_release.zip
```
Expected outcome: Plugin error from taxa: Sample IDs found in the table are missing in the metadata: {'AN77'}.
