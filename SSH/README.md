#  TUTORIAL for connecting to a remote machine

## Remote ssh connection for computing

- Retrieve the encrypted password (from the link provided by the server administrator; do not close the page as it is only valid once)

- Type the command in a terminal and enter the password

```bash
# Execute this command locally to connect to the remote machine
ssh <login>@<machine_name>.imag.umontpellier.fr
```
where `<login>` is your login and `<machine_name>` is the name of the machine (e.g., `oban`).

- To avoid retyping the password for each connection, generate an SSH key locally (if you don't have one already):
    - Check if you already have an SSH key
```bash
# Execute this command locally
ls ~/.ssh/*.pub
```

```bash
# Execute this command locally
ssh-keygen -t rsa
```

- Retrieve the content of the .pub file (public key) in the .ssh folder with

```bash
# Execute this command locally
cat <rsa_key_name>.pub
```
where `<rsa_key_name>.pub` is the name of newly made key with `ssh-keygen`

- Then, on a remote, create a .ssh/authorized_keys file and paste your key into it (the output of `cat`). This can be easily done using `nano`. Remember to save the file afterwards.
```bash
# Execute this command remotely 
nano .ssh/authorized_keys
```

You can now connect by simply typing the command

```bash
ssh <login>@<machine_name>.imag.umontpellier.fr
```

## Remote connection from VSCode

- Install the Remote-SSH extension on VSCode: a 'Remote Explorer' icon should appear below the extensions icon

- You should then see the oban remote to which you can connect


- You can now seen the remote `<machine_name>` you wan to connect to.

## Setting your environment

Now you need to configure the Python environment in this remote for instance by creating a micromamba environment. This require an `environment.yml` file of the following kind:

```yaml
name: nom_de_env
channels:
    - pytorch
    - nvidia
    - conda-forge
dependencies:
    - python=3.12
    - numpy
    - pandas
    - scikit-learn
    - matplotlib
    - seaborn
    - plotly
    - notebook
    - dask
    - dask-jobqueue
    - numba
    - pytorch
    - torchvision
    - torchaudio
    - pytorch-cuda=12.4

```
with for instance `nom_de_env` being `pytorch-env`.

- Create and activate your environment with the commands:

```bash
micromamba create -f environment.yml
```

```bash
micromamba activate pytorch-env
```
