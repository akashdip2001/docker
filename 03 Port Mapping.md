## Run Website in Docker-Ubuntu Img --> & Port Mapping (8080)

Clone the repository inside the **Docker Ubuntu container**, set up a simple web server inside the container (like Python's `http.server` or Nginx), expose the container's port to your laptop, and access the site in your browser. Here's how:

---

| [Create a Nginx Docker Custom img](./02%20Docker%20Custom%20Images.md) |
| --- |

---

## **Steps to Run the Project Inside a Docker Ubuntu Container**

### **Step 1: Start a New Ubuntu Container**
Run a new interactive Ubuntu container:

```bash
docker run -it -p 8080:80 ubuntu bash
```

Explanation:
- `-p 8080:80`: Maps port **80** in the container to port **8080** on your host machine.
- `-it`: Starts the container interactively with a terminal.
- `ubuntu`: Uses the Ubuntu image.
- `bash`: Opens a Bash shell inside the container.

---

### **Step 2: Install Necessary Tools in the Container**
Inside the container, you need to install:
1. **Git**: To clone the repository.
2. **Python** (or any other web server): To serve the HTML files.

Run the following commands in the container:

1. Update and install packages:
   ```bash
   apt update
   apt install -y git python3
   ```

2. Verify installations:
   ```bash
   git --version
   python3 --version
   ```

---

### **Step 3: Clone the Repository**
Clone your GitHub repository inside the container:

```bash
git clone https://github.com/akashdip2001/JavaScript.git
```

Navigate to the project directory:

```bash
cd JavaScript/Js\ Projects/Project\ 002\ -\ To\ Do
```

---

### **Step 4: Start a Simple Web Server**
Use Python's built-in `http.server` module to serve the files:

```bash
python3 -m http.server 80
```

This starts a web server on **port 80** inside the container.

---

### **Step 5: Access the Website**
1. Open a browser on your Windows host machine.
2. Navigate to:

   ```
   http://localhost:8080
   ```

Your website should now be visible in the browser.

---

### **Step 6: Optional - Run Container in Detached Mode**
If you want to keep the container running in the background:

1. Exit the interactive session by stopping the server (`Ctrl + C`) and typing `exit`.

2. Start the container in detached mode with the web server running:
   ```bash
   docker run -d -p 8080:80 ubuntu bash -c "apt update && apt install -y git python3 && git clone https://github.com/akashdip2001/JavaScript.git && cd JavaScript/Js\ Projects/Project\ 002\ -\ To\ Do && python3 -m http.server 80"
   ```

---

### **Summary of Commands:**
1. Start the container:
   ```bash
   docker run -it -p 8080:80 ubuntu bash
   ```

2. Install Git and Python:
   ```bash
   apt update && apt install -y git python3
   ```

3. Clone the repository:
   ```bash
   git clone https://github.com/akashdip2001/JavaScript.git
   cd JavaScript/Js\ Projects/Project\ 002\ -\ To\ Do
   ```

4. Start the web server:
   ```bash
   python3 -m http.server 80
   ```

5. Access the site in your browser at `http://localhost:8080`.