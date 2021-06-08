# Build Scripts
 docker build --build-arg ARG_WORKSPACE_FLAVOR=minimal -t gs-mlworkspace-min -f Dockerfile . 

 docker build -t gs-mlworkspace-min-gpu -f gpu-flavor/Dockerfile.min.gpu .

 docker build -t gs-mlworkspace-min-gpu-wsi -f Dockerfile.wsi .

 # Run Scripts
 docker run -d -p 8083:8080 --name "bn-mlworkspace-min01" -v "ml-workspace:/workspace" -v "D:\:/host_Data" -v "/var/run/docker.sock:/var/run/docker.sock" --restart always gs-mlworkspace-min:latest

docker run -d -p 8084:8080 --env NVIDIA_DISABLE_REQUIRE=1 --gpus all --name "bn-mlworkspace-gpu-min" -v "ml-workspace:/workspace" -v "D:\:/host_Data" -v "/var/run/docker.sock:/var/run/docker.sock" --restart always gs-mlworkspace-min-gpu:latest

docker run -d -p 8085:8080 --env NVIDIA_DISABLE_REQUIRE=1 --gpus all --name "bn-mlworkspace-gpu-min-wsi" -v "ml-workspace-test:/workspace" -v "D:\:/host_Data" -v "/var/run/docker.sock:/var/run/docker.sock" --restart always gs-mlworkspace-min-gpu-wsi:latest

# Misc Test Containers
docker run -it --env NVIDIA_DISABLE_REQUIRE=1 --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody
docker run -it --env NVIDIA_DISABLE_REQUIRE=1 --gpus all  pytorch/pytorch:1.6.0-cuda10.1-cudnn7-runtime
docker run -it --env NVIDIA_DISABLE_REQUIRE=1 --gpus all  docker.io/nvidia/cuda:10.2-devel-ubuntu18.04

gs-mlworkspace-min-gpu-wsi:latest

# Push Scripts
docker push gs-mlworkspace-min:latest