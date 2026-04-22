# 🚀 Private Docker Registry with Authentication (DevOps Project)

## 📌 Project Overview
This project demonstrates how to set up a Private Docker Registry using Docker and secure it with authentication. It allows users to store, manage, and retrieve Docker images locally instead of using public registries like Docker Hub.

This project represents a real-world DevOps workflow involving containerization, image management, and secure storage.

## 🎯 Objectives
- Understand Docker workflow
- Create a private Docker registry
- Implement authentication
- Push and pull Docker images
- Verify stored images

## 🛠️ Technologies Used
- Docker
- Ubuntu (WSL)
- Docker Registry
- Apache htpasswd

## 🧠 Key Concepts
- Docker Image: Packaged application
- Docker Container: Running instance of image
- Docker Registry: Storage for images
- Tagging: Naming image for registry

## 🏗️ Architecture
Docker Hub → Local System → Private Registry → Push/Pull Images

## ⚙️ Implementation Steps

1. Install Docker
sudo apt update  
sudo apt install docker.io -y  

2. Start Docker
sudo service docker start  

3. Run Registry
docker run -d -p 5000:5000 --name registry registry:2  

4. Setup Authentication
sudo apt install apache2-utils -y  
mkdir auth  
htpasswd -Bc auth/htpasswd admin  

5. Run Registry with Auth
docker rm -f registry  
docker run -d -p 5000:5000 --name registry -v $(pwd)/auth:/auth -e REGISTRY_AUTH=htpasswd -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -e REGISTRY_AUTH_HTPASSWD_REALM="Registry Realm" registry:2  

6. Pull Image
docker pull ubuntu  

7. Tag Image
docker tag ubuntu localhost:5000/my-ubuntu  

8. Push Image
docker push localhost:5000/my-ubuntu  

9. Pull from Registry
docker pull localhost:5000/my-ubuntu  

10. Verify
curl http://localhost:5000/v2/_catalog  

OR  
curl -u admin:password http://localhost:5000/v2/_catalog  

## 📸 Screenshots
- docker ps
- docker login
- docker push
- docker pull
- curl _catalog output

## 📊 Output
- Private registry created
- Authentication implemented
- Image successfully pushed and pulled
- Verified using API

## 🔐 Security
- Username and password authentication
- Prevents unauthorized access

## 💡 Use Cases
- Private image storage
- DevOps pipelines
- Secure deployments

## 🎤 Conclusion
This project demonstrates a secure and efficient way to manage Docker images using a private registry, which is widely used in DevOps environments.

## 👩‍💻 Author
Sadgi
