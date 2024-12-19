<img align="right" alt="cloud platform" width="300" src="https://github.com/user-attachments/assets/b3ba674a-1ac3-4f01-902c-bb1b1fc02746"> 

Using AWS as your cloud platform to run and expose your Docker container 

## Deploying your Docker container on AWS:

---

### **Step 1: Launch an EC2 Instance**
1. **Login to AWS Management Console**:
   Go to [AWS Console](https://aws.amazon.com/console/).

2. **Navigate to EC2**:
   - Search for **EC2** in the services menu.
   - Click **Launch Instance**.

3. **Configure Instance**:
   - **Name**: Give your instance a name, e.g., `docker-web-server`.
   - **AMI**: Choose the latest **Amazon Linux 2 AMI** or **Ubuntu Server**.
   - **Instance Type**: Select a small instance, such as `t2.micro` (free-tier eligible).
   - **Key Pair**: Create or select an existing key pair for SSH access.
   - **Security Group**: Add a rule to allow:
     - **HTTP (port 80)**
     - **Custom TCP (port 8080)** for your container.
     - **SSH (port 22)** for remote access.
   - Launch the instance.

---

### **Step 2: SSH into the Instance**
1. Use your terminal or an SSH client to connect to your EC2 instance:
   ```bash
   ssh -i "your-key.pem" ec2-user@<your-ec2-public-ip>
   ```

2. Update the system and install Docker:
   ```bash
   sudo yum update -y
   sudo yum install docker -y
   sudo service docker start
   sudo usermod -aG docker ec2-user
   ```
   Log out and log back in to apply group changes.

---

### **Step 3: Pull Your Docker Image**
1. Log in to Docker Hub from your EC2 instance:
   ```bash
   docker login
   ```

2. Pull your Docker image:
   ```bash
   docker pull akashdip2001x/todo-app-from-github:latest
   ```

---

### **Step 4: Run the Docker Container**
Run your container with port mapping to expose it:
```bash
docker run -d -p 8080:80 akashdip2001x/todo-app-from-github:latest
```
Here:
- `-d`: Detached mode.
- `-p 8080:80`: Maps container port 80 to host port 8080.

---

### **Step 5: Test the Deployment**
1. **Get Public IP**:
   Find the public IP of your EC2 instance in the AWS Console.

2. **Access the Website**:
   Open your browser and visit:
   ```
   http://<your-ec2-public-ip>:8080
   ```

---

### **Step 6: Persist Changes (Optional)**
If you restart the EC2 instance, Docker might not start automatically. To ensure it does:
1. Enable Docker to start at boot:
   ```bash
   sudo systemctl enable docker
   ```
2. Add a startup script to re-run your container:
   - Create a script:
     ```bash
     sudo nano /etc/systemd/system/todo-app.service
     ```
   - Add the following content:
     ```ini
     [Unit]
     Description=Run Docker container for Todo App
     After=docker.service

     [Service]
     Restart=always
     ExecStart=/usr/bin/docker run -d -p 8080:80 akashdip2001x/todo-app-from-github:latest

     [Install]
     WantedBy=multi-user.target
     ```
   - Reload and enable the service:
     ```bash
     sudo systemctl daemon-reload
     sudo systemctl enable todo-app.service
     ```

---

### **Step 7: Enhance Access**
- **Use a Custom Domain**: Point a domain name to the EC2 instance's public IP via DNS.
- **Enable HTTPS**: Install NGINX or Apache with Let's Encrypt for secure HTTPS access.

---

[<img align="left" alt="DigitalOcean" width="300" src="https://github.com/user-attachments/assets/62c310b6-5be2-488a-8a08-d0e6719fb2d8">](./03%20Push%20in%20Docker%20Hub.md)

---

