## Install minkube

## Install kubectl

1. Download the latest release with the command:
```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

2. Validate the binary (optional)
```bash
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

2.1 Validate the kubectl binary against the checksum file:
```bash
   echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

3. Install kubectl
```bash
  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
4. Test to ensure the version you installed is up-to-date:
```bash
  kubectl version --client
```

4.1 Or use this for detailed view of version:
```bash
  kubectl version --client --output=yaml
```