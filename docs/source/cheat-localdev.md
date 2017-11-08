# Cheatsheet: Local development using minikube

After [installing minikube](https://github.com/kubernetes/minikube#installation):

```bash
minikube start
eval $(minikube docker-env)  # use docker daemon inside minikube

git clone git@github.com:jupyterhub/zero-to-jupyterhub-k8s.git
cd zero-to-jupyterhub-k8s
python3 -m venv .            # create virtual environment
pip install ruamel.yaml      # install dependency

# build docker images in minikube
./build.py build

# edit minikube-conf.yaml, and, if desired, create an additional file { -f config.yaml }
helm upgrade --wait --install --namespace=hub hub jupyterhub/ -f minikube-config.yaml

minikube service --namespace=hub proxy-public
```
