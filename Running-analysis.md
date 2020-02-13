Install ampliseq workflow
```
wget https://github.com/nf-core/ampliseq/archive/master.zip
mkdir -p ~/my-pipelines/nf-core/
unzip master.zip -d ~/my-pipelines/nf-core/
```

Edit config files for pipeline - NB not sure if these settings are required. Suggest trying to download and run the pipeline without these modifications and delete this section if it runs fine. 

in file nextflow.config modify..

```
docker.temp = 'auto'
    env {
      JOBLIB_TEMP_FOLDER="/data/tmp"
    }
```
in file conf/base.config modify..

```
  withName: make_SILVA_132_16S_classifier {
    cpus = { check_max (28 * task.attempt, 'cpus' ) }
    memory = { check_max (220.GB * task.attempt, 'memory' ) }
    time = { check_max (12.h * task.attempt, 'time' ) }
  }

```
Configure required system variables for analysis pipeline

```
export TMPDIR=/data/tmp
export NXF_TEMP=/data/tmp
export NXF_WORK=/data/work
```

Running analysis pipeline

```
nextflow run main.nf \
    -profile conda \
    --reads "/path/to/folder" \
    --FW_primer AGGATTAGATACCCTGGTA \
    --RV_primer CRRCACGAGCTGACGAC \
    --metadata "/path/to/file" \
    --reference_database Silva_132_release.zip
```
Expected outcome: runs successfully with single sample (AN77)from data set. Retest with multiple samples. 


Running analysis pipeline with pre-existing classfier

NB gives faster run times but need to ensure you use a compatible classifier.  

```
nextflow run main.nf \
    -profile conda \
    --reads datasub \
    --FW_primer AGGATTAGATACCCTGGTA \
    --RV_primer CRRCACGAGCTGACGAC \ 
    --metadata metadata.tsv 
    --reference_database Silva_132_release.zip \
    --classifier "AGGATTAGATACCCTGGTA-CRRCACGAGCTGACGAC-99-classifier.qza" \ --trunclenf 212 \
    --trunclenr 175
```
Expected outcome: runs successfully with subset of full data set (ie samples 10,22,27,40,45,48,58,66). errors on full 23 samples including controls. Outcome seems to be sensitive to trunclenf/r parameters. Need to get input from someone with more knowledge of Qiime and illumina sequencing to ensure these settings are appropriate. 



