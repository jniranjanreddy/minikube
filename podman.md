```

Install Podman in a WSL distro (e.g., Ubuntu) as above, then enable systemd if needed: 
sudo systemctl enable --now podman.socket.


check latest version
curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64  # Adjust for your arch (e.g., arm64)
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version  # Verify

minikube start --driver=podman --container-runtime=cri-o


```
