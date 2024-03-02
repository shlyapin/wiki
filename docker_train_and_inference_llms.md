---
title: Docker
layout: page
permalink: /docker_train_and_inference_llms
---

# Introduction

[Link to GitHub with Dockerfile, requirements.txt, and the instructions](https://github.com/alshlyapin/docker_train_and_inference_llms)

Docker enables you to run containers, packaging an application along with its dependencies. The primary issue Docker addresses is the common problem where code may not work on another computer. By isolating the application, Docker also minimizes the risk of causing issues on the host system.

- **Docker Host**: The machine (either physical or virtual) where Docker is installed and runs.
- **Docker Guest**: The containers managed by the Docker host, each providing a separate, isolated environment for running applications.

This instruction applies specifically to the Dockerfile I provided and may differ with other Dockerfiles. The provided Dockerfile is tailored for training and inferencing Large Language Models (LLMs) using Hugging Face transformers, but it is not limited to this use case. The container includes Hugging Face transformers and PyTorch.

# Installation

To install Docker on Ubuntu, follow these instructions:
- https://docs.docker.com/engine/install/ubuntu/
- https://docs.docker.com/engine/install/linux-postinstall/

If you succeeded, you can run `docker run hello-world`, and it will print a text starting with "Hello from Docker!"

To make Docker work with Nvidia GPUs, follow these instructions:
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/sample-workload.html

If you succeeded, you can run `sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi`, and it will print a table with GPUs.

# Build the Image

To build the image, run the following command from the folder containing the Dockerfile:

```
docker build -t train_and_inference_llms .
```

If you need a newer version of a Docker image from Hugging Face or a new library version specified in `requirements.txt`, run:

```
docker build --no-cache -t train_and_inference_llms .
```

This command builds the image from scratch, ensuring the latest versions are included.

# Start the Container

```
docker run --name train_and_inference_llms_container \
  --interactive --tty --detach --restart=unless-stopped \
  --runtime=nvidia --gpus all \
  --mount type=bind,source=/home/my_user/code,target=/code \
  train_and_inference_llms
```

- `train_and_inference_llms_container`: Name of the container (you can choose any name you like).
- `/home/my_user/code`: A folder on the host. `/code` is where this folder will be inside the guest. Changes made in `/code` on the guest are reflected in `/home/my_user/code` on the host, and vice versa.
- You can mount other folders following the format of the previous point.
- `train_and_inference_llms`: The name of the image (from the "Build the Image" section).

# VS Code

1. Install the Docker extension by Microsoft.
2. To open a container in VS Code, use the Command Palette -> Dev Containers: Attach to Running Container...

Remember, the code will be located in the `/code` folder.

# Open the Terminal of the Guest from the Host Terminal

```
docker attach train_and_inference_llms_container
```

# Modify the Image

To modify the image, you can either:
- Modify `requirements.txt` for Python library changes.
- Modify the Dockerfile for Ubuntu package changes, e.g., add the line `RUN apt-get install -y vim`.

To use a container with the new image, you need to stop and remove the previous container.

To stop the container:

```
docker stop train_and_inference_llms_container
```

To remove the container:

```
docker rm train_and_inference_llms_container
```
