# 

### 1
Search Well Known Lables in Official Documetation to find the available keys used in labels


For example 
https://kubernetes.io/docs/reference/labels-annotations-taints/#kubernetesiohostname




### 2
If the PVC is in **pending state**, most likely you forgot to mention the Persistent Volume (PV) i.e ```volumeName``` in the Pesistent Volume Claim (PVC) 