## Run your HTML, CSS, and JavaScript project in **Docker** and expose it to your local browser in Windows

---

| [Run Website insite Docker & Expose port 8080](./03%20Port%20Mapping.md) |
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