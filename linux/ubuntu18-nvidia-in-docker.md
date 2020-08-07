Ubuntu 18 NVIDIA CUDA in Docker with GPU support
================================================

# NVIDIA driver installation 

Check here for the mapping: https://docs.nvidia.com/deploy/cuda-compatibility/index.html

        CUDA Toolkit 		Linux x86_64 Driver Version
        CUDA 11.0 (11.0.171) 	>= 450.36.06
        CUDA 10.2 (10.2.89) 	>= 440.33
        CUDA 10.1 (10.1.105) 	>= 418.39
        CUDA 10.0 (10.0.130) 	>= 410.48
        CUDA 9.2 (9.2.88) 	>= 396.26
        CUDA 9.1 (9.1.85) 	>= 390.46
        CUDA 9.0 (9.0.76) 	>= 384.81

I need CUDA 10.0 right now. It seems that I can just grab the latest driver as that appears to be backwards compatible with CUDA 10.0.

	sudo apt update
	sudo apt upgrade -y

Take a look what's there:

	sudo apt list |grep ^nvidia-driver

I will pick `nvidia-driver-440`.

	sudo apt install nvidia-driver-440
	sudo reboot
	nvidia-smi  # Verify that driver is loaded and GPU is found

The CUDA toolkit will be installed *inside* the container. `nvidia-smi` shows CUDA version 10.2, but apparently that will work fine with CUDA toolkit 10.0.

# Docker installation

	sudo apt install docker.io
	sudo adduser ubuntu docker

Log out and log back in. Verify docker access:

	docker ps

# NVIDIA-docker installation

Continuing with instructions here: https://github.com/NVIDIA/nvidia-docker

	# Add the package repositories
	distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
	curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
	curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

	sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
	sudo systemctl restart docker

# Test GPU access from within container

	docker run --gpus all nvidia/cuda:10.0-base nvidia-smi

