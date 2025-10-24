First install the zigchain by official website of it.

Test it locally

Then go to the directory open the folder in the code editor

Check the "go" folder in your system. copy that entire folder and paste on the zigchaind folder as a directory.

Create the another folder "zigchain-docker"

Add the Dockerfile in it 

Make a directory "k8s" in zigchain-docker which contains the kuberentes files.

Commands:

mkdir ~/zigchain-docker   #make a Directory
cd ~/zigchain-docker      #Enter in a Directory

cp ~/go/bin/zigchaind ./zigchaind  #copy the binary file and node folder
cp -r ~/.zigchain ./zigchain-data

# login to docker Hub by using username and token access not password
docker login

# Build the image in Docker Hub
docker build -t your_dockerhub_username/zigchain-node:latest .

# Push the image in Docker hub
docker push your_dockerhub_username/zigchain-node:latest

# Run the container of Docker Hub
docker run -d \
  --name zigchain-node \
  -p 26656:26656 \
  -p 26657:26657 \
  -p 1317:1317 \
  your_dockerhub_username/zigchain-node:latest
  
# Check the logs of node in the server
docker logs -f zigchain-node

# Deploy on the server
kubectl apply -f zigchain-node-deployment.yaml
kubectl get pods
kubectl logs -f zigchain-node-xxxxx
kubectl get pods
kubectl logs -f <pod-name>
kubectl get svc

