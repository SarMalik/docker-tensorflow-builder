# Compile Tensorflow on Docker

Docker images to compile TensorFlow yourself.

Tensorflow only provide a limited set of build and it can be challenging to compile yourself on certain configuration. With this `Dockerfile`, you should be able to compile TensorFlow on any Linux platform that run Docker.

Compilation images are provided for Ubuntu 18.10, Ubuntu 16.04, CentOS 7.4 and CentOS 6.6.

## Requirements

- `docker`
- `docker-compose`

## Usage

- Clone this repository:

```bash
git clone https://github.com/hadim/docker-tensorflow-builder.git
```

### TensoFlow CPU

- Edit the `build.sh` file to modify TensorFlow compilation parameters. Then launch the build:

```bash
LINUX_DISTRO="ubuntu-16.04"
# or LINUX_DISTRO="ubuntu-18.10"
# or LINUX_DISTRO="centos-7.4"
# or LINUX_DISTRO="centos-6.6"
cd "tensorflow/$LINUX_DISTRO"

# Set env variables
export PYTHON_VERSION=3.6
export TF_VERSION_GIT_TAG=v1.13.1
export BAZEL_VERSION=0.19
export USE_GPU=0

# Build the Docker image
docker-compose build

# Start the compilation
docker-compose run tf

# You can also do:
# docker-compose run tf bash
# bash build.sh
```

### TensorFlow GPU

- Edit the `build.sh` file to modify TensorFlow compilation parameters. Then launch the build:

```bash
LINUX_DISTRO="ubuntu-16.04"
# or LINUX_DISTRO="ubuntu-18.10"
# or LINUX_DISTRO="centos-7.4"
# or LINUX_DISTRO="centos-6.6"
cd "tensorflow/$LINUX_DISTRO"

# Set env variables
export PYTHON_VERSION=3.6
export TF_VERSION_GIT_TAG=v1.13.1
export BAZEL_VERSION=0.19
export USE_GPU=1
export CUDA_VERSION=10.0
export CUDNN_VERSION=7.5
export NCCL_VERSION=2.4

# Build the Docker image
docker-compose build

# Start the compilation
docker-compose run tf

# You can also do:
# docker-compose run tf bash
# bash build.sh
```

---

- Refer to [tested build configurations](https://www.tensorflow.org/install/source#tested_build_configurations) to know which `BAZEL_VERSION` you need.
- Be patient, the compilation can be long.
- Enjoy your Python wheels in the `wheels/` folder.
- *Don't forget to remove the container to free the space after the build: `docker-compose rm --force`.*

## Builds

| Tensorflow | Python | Distribution | Bazel | CUDA | cuDNN | NCCL | Comment |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2.0.1 | 3.6.8 | Ubuntu 18.04 | 0.24.1 | 10.0 | 7.5 | 2.4 | OK |
| 2.0.1 | 3.6.8 | Ubuntu 18.04 | 0.24.1 | - | - | - | OK |
| v2.0.0-alpha0 | 3.6 | Ubuntu 18.10 | 0.20 | 10.0 | 7.5 | 2.4 | seg fault error  |
| v2.0.0-alpha0 | 3.6 | Ubuntu 18.10 | 0.20 | - | - | - | OK |
| v2.0.0-alpha0 | 3.6 | Ubuntu 16.04 | 0.20 | 10.0 | 7.5 | 2.4 | TODO |
| v2.0.0-alpha0 | 3.6 | Ubuntu 16.04 | 0.20 | - | - | - | TODO |
| 1.9.0 | 3.6 | Ubuntu 16.04 | - | - | 0.19 | - | OK |
| 1.9.0 | 3.6 | Ubuntu 16.04 | 0.19 | 9.0 | 7.1 | - | OK |
| 1.9.0 | 3.6 | Ubuntu 16.04 | 0.19 | 9.1 | 7.1 | - | OK |
| 1.9.0 | 3.6 | Ubuntu 16.04 | 0.19 | 9.2 | 7.1 | - | OK |
| 1.9.0 | 3.6 | CentOS 6.6 | - | 0.19 | - | - | OK |
| 1.9.0 | 3.6 | CentOS 6.6 | 0.19 | 9.0 | 7.1 | - | OK |
| 1.9.0 | 3.6 | CentOS 6.6 | 0.19 | 9.1 | 7.1 | - | OK |
| 1.9.0 | 3.6 | CentOS 6.6 | 0.19 | 9.2 | 7.1 | - | OK |
| 1.15.0 | 3.7.5 | Ubuntu 18.04 | 0.24.1 | - | - | - | seg fault error |
| 1.15.0 | 3.6 | Ubuntu 18.04 | 0.24.1 | - | - | - | seg fault error |
| 1.15.0 | 3.6.12 | Ubuntu 18.04 | 0.26.1 | 10.2 | 7.6 | 2.1 | OK |
| 1.15.0 | 3.6.12 | Ubuntu 18.04 | 0.26.1 | - | - | - | OK |


## Forked project authors

- Hadrien Mary <hadrien.mary@gmail.com>

## Authors

- Dimitri Gerin <dimitri.gerin@gmail.com>

## Usage

- Clone this repository:

```bash
git clone https://github.com/hadim/docker-tensorflow-builder.git
```

- Clone tensorflow project inside docker-tensorflow-builder (example with https://github.com/Dimitri1/tensorflow-quant)

```bash
cd docker-tensorflow-builder
git clone https://github.com/Dimitri1/tensorflow-quant tensorflow
```
- build

```bash
bash build.sh
```

## License

MIT License. See [LICENSE](LICENSE).
