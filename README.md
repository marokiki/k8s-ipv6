# k8s-ipv6
```
sudo sysctl -w net.ipv6.conf.all.forwarding=1
sudo kubeadm init --config=init/akatsuki-1.yaml
```
## join 
```
echo "apiVersion: kubeadm.k8s.io/v1beta3
kind: JoinConfiguration
discovery:
  bootstrapToken:
    apiServerEndpoint: 192.168.20.111:6443
    token: "clvldh.vjjwg16ucnhp94qr"
    caCertHashes:
    - "sha256:a4863cde706cfc580a439f842cc65d5ef112b7b2be31628513a9881cf0d9fe0e"
    # change auth info above to match the actual token and CA certificate hash for your cluster
nodeRegistration:
  kubeletExtraArgs:
    node-ip: 192.168.20.114,240b:250:9800:4a20::114" > kubeadm-join.yaml
sudo kubeadm join --config=kubeadm-join.yaml
```
```
export GITHUB_TOKEN=github_pat_*****                 
export GITHUB_USER=segre5458  
# kubernetes/で実行
flux bootstrap github --owner=$GITHUB_USER --repository=k8s-ipv6 --branch=master --path=./k8s-ipv6/_flux/akatsuki --personal --components-extra=image-reflector-controller,image-automation-controller --reconcile
wget https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl apply -f kube-flannel.yml
```

