1. [x] [Push in Docker Hub](https://hub.docker.com/r/akashdip2001x/todo-app-from-github)
2. [x] Access website via Docker in AWS
3. [x] Deploy in DigitalOcean

---

## To push a Docker container to your Docker Hub repository
<img align="right" alt="Docker Hub" width="300" src="https://github.com/user-attachments/assets/f30947aa-0632-470c-bf98-3a7908b69348"> 

<details>	
     <summary><b>img of website</b></summary><br>
   
![Screenshot (684)](https://github.com/user-attachments/assets/ae7592de-a0a5-4668-aa39-5fec37cd15b6)
</details>

---

### **Step 1: Prepare Your Docker Hub Account**
1. **Login to Docker Hub**:
   - Ensure you have a Docker Hub account. If not, create one at [https://hub.docker.com](https://hub.docker.com).
   - Log in from your terminal:
     ```bash
     docker login
     ```
   - Enter your Docker Hub username and password when prompted.

2. **Create a Repository on Docker Hub**:
   - Visit [Docker Hub](https://hub.docker.com).
   - Click on **Repositories > Create Repository**.
   - Name the repository (e.g., `todo-app-from-github`).
   - Leave the visibility as **Public** or set it to **Private**, depending on your preference.

<p aline=""center>
<img src="https://github.com/user-attachments/assets/dcbe44cf-a67e-410e-85bf-852b29686c99" width="45%">
<img src="https://github.com/user-attachments/assets/51b93f10-ed3e-4df4-91c9-a97aeb8348d3" width="45%">
</p>

---

### **Step 2: Tag the Docker Container**
Docker requires containers to have a tag associated with a Docker Hub repository name before pushing.

1. Identify the container image to tag:
   ```bash
   docker images
   ```

   Example output:
   ```
   REPOSITORY          TAG       IMAGE ID       CREATED          SIZE
   ubuntu              latest    6c6e7a7d404d   2 weeks ago      29MB
   ```

2. Tag the image:
   ```bash
   docker tag <image-id> akashdip2001x/todo-app-from-github:tagname
   ```

   Replace `<image-id>` with the `IMAGE ID` of your container. For example:
   ```bash
   docker tag 6c6e7a7d404d akashdip2001x/todo-app-from-github:latest
   ```
![Screenshot (691)](https://github.com/user-attachments/assets/8c9e77cb-aa76-4f15-bbfb-e160f9004af6)

---

### **Step 3: Push the Container**
Push the tagged image to Docker Hub:
```bash
docker push akashdip2001x/todo-app-from-github:latest
```
![Screenshot (692)](https://github.com/user-attachments/assets/7a3b3cf1-68d8-428a-9625-0c6823362139)

---

### **Step 4: Verify on Docker Hub**
1. Go to your Docker Hub repository: [https://hub.docker.com/r/akashdip2001x/todo-app-from-github](https://hub.docker.com/r/akashdip2001x/todo-app-from-github).
2. Ensure the pushed image is visible.

![Screenshot (692)](https://github.com/user-attachments/assets/40e24404-deaf-4f7a-a9ca-e3dd569f5175)

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

<img align="right" alt="cloud platform" width="300" src="https://github.com/user-attachments/assets/b3ba674a-1ac3-4f01-902c-bb1b1fc02746"> 

Access the website via Docker when the container is downloaded to a cloud platform or any other machine:

---

### **1. Push the Image to the Cloud**
You've already pushed the Docker image to Docker Hub (`akashdip2001x/todo-app-from-github:latest`). Now you can:
- Pull the image on any cloud server.
- Run the container with port mapping to expose the website.

---

### **2. Steps to Run the Container in the Cloud**

#### **Step 1: Set Up a Cloud Server**
- Provision a server on a cloud provider (AWS, Google Cloud, Azure, etc.) or use a private server.
- Make sure Docker is installed and running on the server.

#### **Step 2: Pull the Docker Image**
Log in to the server and pull the image:
```bash
docker pull akashdip2001x/todo-app-from-github:latest
```

#### **Step 3: Run the Docker Container**
Run the container with port mapping:
```bash
docker run -d -p 8080:80 akashdip2001x/todo-app-from-github:latest
```
Here:
- `-d`: Runs the container in detached mode.
- `-p 8080:80`: Maps port 80 inside the container to port 8080 on the cloud server.

---

### **3. Access the Website**

#### **Step 1: Get the Public IP Address**
Find the public IP of your cloud server. For example:
- AWS EC2: Check the "Public IPv4 Address" in the AWS Management Console.
- Other providers: Refer to their respective dashboards for the public IP.

#### **Step 2: Access the Website**
Open a browser on your local machine or phone, and navigate to:
```
http://<server-public-ip>:8080
```
Replace `<server-public-ip>` with the actual IP address of your cloud server.

---

### **4. (Optional) Secure the Setup with a Domain Name**
1. **Get a Domain**:
   Purchase or use an existing domain name.
2. **Point Domain to Server**:
   Update your domain's DNS settings to point to the server's public IP.
3. **Use HTTPS**:
   Use a reverse proxy like NGINX and tools like Let's Encrypt to enable HTTPS.

---

### **5. ⚠️ Alternative: Run on Local Machine and Use Tunneling (Port Forwarding)**
If you're running the container on your laptop and want external access:
1. Use a tunneling service like **ngrok**:
   ```bash
   ngrok http 8080
   ```
2. Share the URL provided by `ngrok` to access the website from anywhere.

---

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

<img align="right" alt="DigitalOcean" width="300" src="https://github.com/user-attachments/assets/62c310b6-5be2-488a-8a08-d0e6719fb2d8"> 

DigitalOcean is an excellent platform for deploying Docker containers. Here's a step-by-step guide on how to **run your Docker container** and access the website through the **DigitalOcean Droplet**.

---

## **Steps to Deploy Your Docker Image on DigitalOcean**

### **1. Create a Droplet on DigitalOcean**
1. Log in to [DigitalOcean Dashboard](https://cloud.digitalocean.com/).
2. Click on **Create** → **Droplets**.
3. Choose the **Ubuntu** operating system (recommended for Docker).
4. Select a plan (basic $5/month works fine for testing purposes).
5. Choose a region close to your location for low latency.
6. Add an SSH key (for secure access) or choose a password-based login.
7. Click **Create Droplet**.

---

### **2. Connect to Your Droplet**
- If you added an SSH key:
   ```bash
   ssh root@<your-droplet-ip>
   ```
- If you're using a password, log in with the **IP address** and root credentials provided by DigitalOcean.

---

### **3. Install Docker on the Droplet**
Run the following commands to set up Docker:

1. **Update the system**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Install Docker**:
   ```bash
   sudo apt install -y docker.io
   ```

3. **Start Docker and enable it on boot**:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. **Verify Docker is installed**:
   ```bash
   docker --version
   ```

---

### **4. Pull and Run Your Docker Image**
Now that Docker is installed on the Droplet:

1. **Pull your Docker image** from Docker Hub:
   ```bash
   docker pull akashdip2001x/todo-app-from-github:latest
   ```

2. **Run the container with port mapping**:
   ```bash
   docker run -d -p 8080:80 akashdip2001x/todo-app-from-github:latest
   ```
   - `-d` runs the container in the background.
   - `-p 8080:80` maps port `80` of the container to port `8080` of the Droplet.

3. **Verify the container is running**:
   ```bash
   docker ps
   ```

---

### **5. Access the Website**
1. Find your Droplet's **public IP address** on the DigitalOcean dashboard.
2. Open a browser on your laptop or phone and visit:
   ```
   http://<your-droplet-ip>:8080
   ```
   Replace `<your-droplet-ip>` with the actual IP address.

---

## **Optional Enhancements**

### **Secure the Website with HTTPS**
To enable HTTPS, you can use a reverse proxy like **NGINX** with **Let’s Encrypt**:
1. Install NGINX on the Droplet.
2. Use Let's Encrypt to issue a free SSL certificate.
3. Configure NGINX as a reverse proxy to forward traffic to your Docker container.

---

### **Use a Custom Domain**
1. Purchase a domain (e.g., from Namecheap, GoDaddy).
2. Point your domain’s DNS records to the Droplet's public IP address.
3. Update your NGINX or web server configuration to serve the website under the domain.

---

## **Quick Recap**
1. Create a Droplet on DigitalOcean.
2. Install Docker and pull your image from Docker Hub.
3. Run the container with port mapping (`-p 8080:80`).
4. Access the website via the Droplet’s public IP.




