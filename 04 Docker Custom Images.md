## Run your HTML, CSS, and JavaScript project in **Docker** and expose it to your local browser in Windows
<img align="right" alt="python_logo" width="300" src="https://github.com/user-attachments/assets/72c70664-38a7-4d80-8fc2-b4b40c2ead26"> 

---

| [Run Website insite Docker & Expose port 8080](./02%20Host%20HTML%20website.md) |
| --- |

---

## **Steps to Run Your HTML, CSS, JavaScript Project in Docker**

### **Step 1: Clone Your Repository**
First, clone your GitHub repository into your WSL (Kali Linux) environment or download it directly:

```bash
git clone https://github.com/akashdip2001/JavaScript.git
```

Change the directory to the project's location:
```bash
cd JavaScript/Js\ Projects/Project\ 002\ -\ To\ Do
```

---

### **Step 2: Create a Dockerfile**
To serve your website, you need a simple HTTP server. Let's use an **Nginx server** to host your project.

1. **Create a new file** named `Dockerfile` in the project directory:
   ```bash
   nano Dockerfile
   ```

2. Add the following content to the `Dockerfile`:
   ```Dockerfile
   # Use the official Nginx image
   FROM nginx:latest

   # Copy website files to the Nginx default HTML directory
   COPY . /usr/share/nginx/html

   # Expose port 80 for HTTP traffic
   EXPOSE 80

   # Start Nginx server
   CMD ["nginx", "-g", "daemon off;"]
   ```

   - This will use the Nginx image to serve your project files and expose **port 80**.

3. Save and close the `Dockerfile` (`Ctrl + O` to save and `Ctrl + X` to exit).

---

### **Step 3: Build the Docker Image**
To build the Docker image for your website, run this command inside the project directory:

```bash
docker build -t todo-app .
```

- `-t todo-app` is the name/tag of the image.
- The `.` at the end refers to the current directory where the `Dockerfile` exists.

---

### **Step 4: Run the Docker Container**
Run the Docker container and expose port **80** inside the container to port **8080** on your Windows host:

```bash
docker run -d -p 8080:80 --name todo-container todo-app
```

Explanation:
- `-d`: Runs the container in detached mode (in the background).
- `-p 8080:80`: Maps port **80** (inside the container) to port **8080** (on your localhost).
- `--name todo-container`: Gives the container a name (`todo-container`).
- `todo-app`: Name of the Docker image you just built.

---

### **Step 5: Verify the Container**
Check that your container is running:

```bash
docker ps
```

You should see your container listed and running.

---

### **Step 6: Access Your Website**
1. Open a browser on your Windows machine.
2. Go to the following URL:

   ```
   http://localhost:8080
   ```

Your website should now be running and visible in the browser.

---

### **Additional Commands**:

1. **Stop the Container**:
   ```bash
   docker stop todo-container
   ```

2. **Start the Container Again**:
   ```bash
   docker start todo-container
   ```

3. **Remove the Container**:
   ```bash
   docker rm todo-container
   ```

4. **Remove the Docker Image**:
   ```bash
   docker rmi todo-app
   ```

---

### **Summary**:
- **Build**: `docker build -t todo-app .`
- **Run**: `docker run -d -p 8080:80 --name todo-container todo-app`
- **Access**: Open `http://localhost:8080` in your browser.

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

<img align="right" alt="python_logo" width="300" src="https://github.com/user-attachments/assets/b3ba674a-1ac3-4f01-902c-bb1b1fc02746"> 

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
