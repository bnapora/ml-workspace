# Instructions for Creating Various mlworkspace environments  
    - Last updated: 060821

### Container Registry: gestaltml.azurecr.io

## Create Volume
    docker volume create  "ml-workspace"

## Create mlworkspace Flavors
### mlworkspace-min - Size=3.8 GB  
    Docker Build Command:  
     docker build --build-arg ARG_WORKSPACE_FLAVOR=minimal -t gs-mlworkspace-min -f Dockerfile . 
    Docker Run Command:  
     docker run -d -p 8080:8080 --name "[Container Name]" -v "[Volume Name]:/workspace" -v "D:\:/host_Data" -v "/var/run/docker.sock:/var/run/docker.sock" --restart always gestaltmldev.azurecr.io/gs-mlworkspace-min:latest  

### mlworkspace-min-gpu - Size=10.2GB
    Docker Build Command:  
     docker build -t gs-mlworkspace-min-gpu -f gpu-flavor/Dockerfile.min.gpu . 
    Docker Run Command:  
     docker run -d -p 8084:8080 --env NVIDIA_DISABLE_REQUIRE=1 --gpus all --name "[Container Name]" -v "[Volume Name]:/workspace" -v "D:\:/host_Data" -v "/var/run/docker.sock:/var/run/docker.sock" --restart always gestaltmldev.azurecr.io/gs-mlworkspace-min-gpu:latest

### mlworkspace-min-gpu-wsi - Size=16.1 GB
    Docker Build Command:  
     docker build -t gs-mlworkspace-min-gpu-wsi -f Dockerfile.wsi 
    Docker Run Command:  
     docker run -d -p 8084:8080 --env NVIDIA_DISABLE_REQUIRE=1 --gpus all --name "[Container Name]" -v "[Volume Name]:/workspace" -v "D:\:/host_Data" -v "/var/run/docker.sock:/var/run/docker.sock" --restart always gs-mlworkspace-min-gpu-wsi:latest  

### Push mlworkspace images to gestaltmldev.azurecr.io  
    docker push gestaltmldev.azurecr.io/gs-mlworkspace-min:latest <
    docker push gestaltmldev.azurecr.io/gs-mlworkspace-min-gpu:latest

## Other Repositories with Potnetial Docker Images
https://github.com/chenjr0719/Docker-Ubuntu-Unity-noVNC  
- noVNC with Unity Desktop