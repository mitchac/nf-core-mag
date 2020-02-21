Change to the drive where the drive is attached..

```
cd /data 
```

Configuration of B2 cloud storage

```
rclone config
```

Select following options

1. Create new remote: n
2. Name the remote: remote
3. Blackbaze: b2 or 3 
4. Account ID: **get this from an emri team member**
5. Key: **get this from an emri team member**
6. Endpoint: enter
7. Y
8. Quit: q


Copy files from source to destination using the following pattern..
rclone copy remote:$remotename/path/to/sourcefile path/to/filedestination

```
rclone copy b2:emri-files/projects/nextflow-test/metadata.tsv .
rclone copy b2:emri-files/projects/nextflow-test/data data
rclone copy b2:emri-files/projects/nextflow-test/inputs .

```
Expected outcome: Files required for the ampliseq analysis present on the cloud computer
