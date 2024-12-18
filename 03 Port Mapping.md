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

![Screenshot (671)](https://github.com/user-attachments/assets/02462f6a-a1d8-4921-ab77-3ddd23ab678e)

<details>	
     <summary><b>image Guide</b></summary><br>
  🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
   
   ![Screenshot (672)](https://github.com/user-attachments/assets/ead977a9-ed32-4b53-944e-93c65d880ade)
  🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
</details>

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
   <details>	
     <summary><b>image Guide</b></summary><br>
   🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
      
   ![Screenshot (673)](https://github.com/user-attachments/assets/449f4893-310a-40ae-b718-c9d6cb0ed7e8)
   ![Screenshot (674)](https://github.com/user-attachments/assets/ce401b80-bd72-4ec8-b16b-c8a8b54d9743)
   ![Screenshot (675)](https://github.com/user-attachments/assets/a611d16a-3018-4d97-b137-6d55e23d7553)
   ![Screenshot (676)](https://github.com/user-attachments/assets/d8ca25ca-dc96-4896-8f2b-e8afacfeec98)
   🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
    </details>

2. Verify installations:
   ```bash
   git --version
   python3 --version
   ```
<details>	
<summary><b>image Guide</b></summary><br>
  🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥

  ![Screenshot (677)](https://github.com/user-attachments/assets/956aad30-c597-4ddf-82ca-f89d317e3246)
🚥🚥🚥🚥🚥🚥🚥🚥🚥🚥
</details>

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

<p align="center">
<img width="40%" src="https://github.com/user-attachments/assets/078282da-8b82-4e16-bb8f-62a11fa4a45c">
<img width="40%" src="https://github.com/user-attachments/assets/47bafe78-d502-4135-a0aa-bd3ca969b71d">
</p>
<p align="center">
<img width="40%" src="https://github.com/user-attachments/assets/600e93e8-3347-48da-b50b-f3f88eb12115">
<img width="40%" src="https://github.com/user-attachments/assets/c00e4150-7aff-4f4a-bbdd-b571d4d17076">
</p>

---

### **Step 6: Optional - Run Container in Detached Mode**
If you want to keep the container running in the background:

1. Exit the interactive session by stopping the server (`Ctrl + C`) and typing `exit`.

2. Start the container in detached mode with the web server running:
   ```bash
   docker run -d -p 8080:80 ubuntu bash -c "apt update && apt install -y git python3 && git clone https://github.com/akashdip2001/JavaScript.git && cd JavaScript/Js\ Projects/Project\ 002\ -\ To\ Do && python3 -m http.server 80"
   ```

---

### 🧪 **Summary of Commands:**
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

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

To access your laptop's localhost (port 8080) from your mobile browser within the same local area network (LAN), you can follow these steps:

---

<img align="right" alt="python_logo" width="300" src="https://github.com/user-attachments/assets/9472d238-3f17-4ea4-a4b8-486438c1b944"> 

## **Steps to Access Laptop's Localhost on Mobile**

### **Step 1: Find Your Laptop's IP Address**
You need the local IP address of your laptop.

1. Open **Command Prompt** (Windows) or Terminal (if in WSL).
2. Run the following command to find your IP address:
   ```bash
   ipconfig
   ```
3. Look for the **IPv4 Address** under the active network adapter (e.g., Wi-Fi). It will look something like:
   ```
   IPv4 Address: 192.168.1.10
   ```

---

### **Step 2: Access the Website from Mobile**
On your mobile device:
1. Open the browser.
2. Enter the following URL in the address bar:
   ```
   http://<laptop-ip>:8080
   ```
   Replace `<laptop-ip>` with the IPv4 address from Step 1. For example:
   ```
   http://192.168.1.10:8080
   ```

---

### **Step 3: Allow Firewall Access (If Necessary)**
If you can't access the website from your mobile, your Windows firewall might be blocking the connection. To allow access:

1. Open **Windows Firewall** settings:
   - Press `Win + R`, type `firewall.cpl`, and press Enter.

2. Click on **Advanced Settings** (on the left panel).

3. Select **Inbound Rules**, and then click on **New Rule** (on the right panel).

4. Configure the new rule:
   - Rule Type: Select **Port**.
   - Protocol and Ports: Select **TCP** and specify **8080**.
   - Action: Select **Allow the connection**.
   - Profile: Select **Private** (so it only applies to trusted networks like your home Wi-Fi).
   - Name: Give the rule a name like `Allow-8080`.

5. Save and apply the rule.

---

### **Step 4: Test the Connection**
Retry accessing the URL on your mobile:
```
http://<laptop-ip>:8080
```

You should now be able to view the website hosted on your laptop from your mobile device.

---

### **Optional: Ensure Port Forwarding is Correct**
If you're using Docker, the container port (`80`) must already be mapped to your laptop's port (`8080`). Since you've done this with `docker run -p 8080:80`, you're good.

---

### **Troubleshooting Tips**:
1. **Ping Test**: From your mobile, verify connectivity to the laptop:
   - Use a ping tool or app to check if `192.168.1.10` (your laptop IP) responds.

2. **Check Docker Container**:
   Ensure the container is running:
   ```bash
   docker ps
   ```
   Confirm it maps port `8080` to port `80` inside the container.

3. **Recheck Firewall**:
   Ensure the firewall rule for port 8080 is applied.

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

## Test using Postman 🚀

![Screenshot (684)](https://github.com/user-attachments/assets/efd2146d-487e-4dcd-b89f-db1c8b03a32b)
![Screenshot (685)](https://github.com/user-attachments/assets/5022f9d9-4e0a-4c0e-a1aa-77c516ea7a80)
![Screenshot (686)](https://github.com/user-attachments/assets/dfb26c3d-a6c5-4e5b-a31a-1b03c7cf355a)

