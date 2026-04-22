# 🚀 Private Docker Registry (DevOps Project)

## 📌 Overview
This project demonstrates how to set up a private Docker registry with authentication. It allows secure storage and retrieval of Docker images locally.

---

## 🎯 Objectives
- Create a private Docker registry
- Implement authentication
- Push and pull Docker images
- Understand DevOps workflow

---

## 🛠️ Tools Used
- Docker
- Ubuntu (WSL)
- Docker Registry
- htpasswd

---

## ⚙️ Steps

### 1. Run Registry
docker run -d -p 5000:5000 --name registry registry:2

### 2. Setup Authentication
mkdir auth  
htpasswd -Bc auth/htpasswd username  

### 3. Run with Auth
docker run -d -p 5000:5000 --name registry \
-v $(pwd)/auth:/auth \
-e REGISTRY_AUTH=htpasswd \
-e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd \
registry:2  

### 4. Push Image
docker pull ubuntu  
docker tag ubuntu localhost:5000/my-ubuntu  
docker push localhost:5000/my-ubuntu  

### 5. Pull Image
docker pull localhost:5000/my-ubuntu  

### 6. Verify
curl -u username:password http://localhost:5000/v2/_catalog  

---

## 📊 Output
- Private registry created
- Image pushed and pulled successfully
- Authentication working

---

## 🔐 Security
Authentication is implemented using username and password.

---

## 🎤 Conclusion
This project shows how to securely manage Docker images using a private registry.

---

## 👩‍💻 Author
Sadgi
