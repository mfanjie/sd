## Instructions
- install GPU driver and cuda toolkit
- install GPU container toolkit, and change containerd runtime to nvidia
- change containerd root to larger disk and restart containerd, kubelet 
- install kubernetes device driver
- build sd image or use existing mfanjie/sd
- deploy stable diffusion by `kubectl apply -f sd-standalone.yaml`