### Build Docker Image
https://github.com/AbdBarho/stable-diffusion-webui-docker/wiki/Setup
### deploy to kubernetes cluster by
`kubectl apply -f ../specs/sd-standalone.yaml`
### check if gpu is working, run the following command inside pod
```
nvidia-smi
```
### download models to local storage
```
/data/local-storage/models
```
