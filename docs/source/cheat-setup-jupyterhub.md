# Cheatsheet: Setting up JupyterHub

## Prepare configuration file `config.yaml`

1. Create a file called `config.yaml`.
2. Create two random hex strings to use as security tokens:

    ```bash
    openssl rand -hex 32
    openssl rand -hex 32
    ```
3. Insert these lines into the `config.yaml` file.
   Substitute each occurrence of `RANDOM_STRING_N ` below with the output of
   `openssl rand -hex 32`.

    *config.yaml* file
    ```yaml
    hub:
      # output of first execution of 'openssl rand -hex 32'
      cookieSecret: "RANDOM_STRING_1"
    proxy:
      # output of second execution of 'openssl rand -hex 32'
      secretToken: "RANDOM_STRING_2"
    ```
4. Save the `config.yaml` file.

## Install JupyterHub

1. From terminal:

    ```bash
    # add jupyterhub helm repository
    helm repo add jupyterhub https://jupyterhub.github.io/helm-chart/
    helm repo update

    # install chart
    helm install jupyterhub/jupyterhub \
        --version=v0.4 \
        --name=<YOUR-RELEASE-NAME> \
        --namespace=<YOUR-NAMESPACE> \
        -f config.yaml

    # check hub and proxy pods are running
    kubectl --namespace=<YOUR_NAMESPACE> get pod

    # find IP to access JupyterHub (external IP for proxy-public service)
    kubectl --namespace=<YOUR_NAMESPACE> get svc
    # alternative verbose command for IP
    # kubectl --namespace=<YOUR_NAMESPACE> describe svc proxy-public
    ```
2. To use JupyterHub:
    - enter external IP for the `proxy-public` service into a browser.
    - entering any username and password combination as JupyterHub is
      running with a default *dummy* authenticator

### Notes

- `--name` For a class called *data8* you might wish set the name to **data8-jupyterhub**. Find out the name by using `helm list`.
- `--namespace`  is to identify a particular application
- We recommend using the same value for `--name` and `--namespace`
- If you get a `release exists` error, then `helm delete --purge <YOUR-RELEASE-NAME>`. Reinstall by repeating this step. If it persists, `kubectl delete <YOUR-NAMESPACE>` and try again.
- If you get a time out error, add a `--timeout=SOME-LARGE-NUMBER` parameter to the `helm install` command.
