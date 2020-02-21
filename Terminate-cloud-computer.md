#### Copy your results 
Copy your results to cloud storage
```
rclone copy results remote:emri-files/projects/nextflow-test/results
```

#### Detach volume from the cloud computer 
Detach volume
```
openstack server remove volume [your-instance-id] \
  [your-volume-id]
```
#### Delete volume from the cloud computer 
Delete volume
```
openstack volume delete [your-volume-id]
```

#### Delete cloud computer 
Delete cloud computer 
```
openstack server delete [your-server-id]