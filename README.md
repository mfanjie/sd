## Instructions
- install GPU driver and cuda toolkit
- install GPU container toolkit
  https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html
```
curl -s -L https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo | \
sudo tee /etc/yum.repos.d/nvidia-container-toolkit.repo
yum install -y nvidia-container-toolkit
```
- change containerd default runtime to nvidia 
```
containerd config default > /etc/containerd/config.toml
nvidia-ctk runtime configure --runtime=containerd
vi  /etc/containerd/config.toml and change default_runtime_name to nvidia
```

install crictl
```
VERSION="v1.26.0" # check latest version in /releases page
wget https://github.com/kubernetes-sigs/cri-tools/releases/download/$VERSION/crictl-$VERSION-linux-amd64.tar.gz
sudo tar zxvf crictl-$VERSION-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-$VERSION-linux-amd64.tar.gz
```
- change containerd root to larger disk and restart containerd, kubelet
```
vi  /etc/containerd/config.toml
and change root value
```
- install kubernetes
```
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
kubeadm init  --kubernetes-version v1.25.2 \
 --pod-network-cidr=192.168.0.0/16 \
  --cri-socket unix:///run/containerd/containerd.sock
mkdir ~/.kube
mv /etc/kubernetes/admin.conf ~/.kube/config

```
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.26.3/manifests/tigera-operator.yaml
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.26.3/manifests/custom-resources.yaml```
```

- install kubernetes device driver
```
kubectl apply -f https://raw.githubusercontent.com/NVIDIA/k8s-device-plugin/v0.14.1/nvidia-device-plugin.yml
```
- build sd image or use existing mfanjie/sd
- deploy stable diffusion by `kubectl apply -f sd-standalone.yaml`