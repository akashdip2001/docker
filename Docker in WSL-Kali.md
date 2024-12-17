# Docker in WLS

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

## 1) install the Docker Desktop for Windows.

check it's install or not?

```bash
docker --version
```
<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

## 2) Open WSL Kali Terminal ==> Docker Desktop automatically detect Kali Terminal

### ✈️ 1. install img in Docker

```bach
docker run ubuntu
```
<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif">

### ✈️ 2. check where are you now ?

### **How to Check Where You Are?**

1. **Inside the Ubuntu Container or WSL Kali?**
   - If you are inside the container, the prompt will likely change, often to something like this:
     ```bash
     root@<container-id>:/#
     ```
     The prompt will typically include the container's ID or hostname and will **not look like your WSL Kali Linux prompt**.

2. **If You Are Still in WSL (Kali Linux):**
   - Your prompt remains as it is:  
     ```bash
     (whitedevil㉿akashdip2001)-[~]
     ```

---

### **Confirm Your Current Environment**
Use the following commands to confirm where you are:

#### a) **To Check if You're in a Container**  
Run this command:
```bash
cat /etc/os-release
```
- **If you're in the container**, it will show:
   ```
   NAME="Ubuntu"
   VERSION="22.04.3 LTS (Jammy Jellyfish)"
   ```

- **If you're in WSL Kali Linux**, it will show:
   ```
   NAME="Kali GNU/Linux"
   VERSION="2024.1"
   ```

#### b) **Exit the Container**
If you're unsure, you can exit a container by typing:
```bash
exit
```
- If you **exit** and the prompt returns to your WSL terminal (Kali Linux), you were inside the container.

---

### **Recap**
1. If your prompt still looks like `(whitedevil㉿akashdip2001)-[~]`, you're in WSL Kali Linux.  
2. Run `cat /etc/os-release` to confirm whether you're in **Ubuntu** (Docker container) or **Kali Linux** (WSL).  
3. When running `docker run`, you interact with the container **through Docker Engine** from WSL.

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

### ✈️ 3. **Check if the Container is Running**


1. **Check running containers:**
   ```bash
   docker ps
   ```

2. **Access a running container:**
   ```bash
   docker exec -it <container_id> bash
   ```

3. **Start a stopped container:**
   ```bash
   docker start <container_id>
   docker exec -it <container_id> bash
   ```

4. **Start a new container with a terminal:**
   ```bash
   docker run -it ubuntu bash
   ```
<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif">

### ✈️ 3.1 Some Time : Not start again normally ==> Try ReStart or Deleate & create a new one


1. List all containers:
   ```bash
   docker ps -a
   ```

2. Restart a stopped container:
   ```bash
   docker start -ai <container_id>
   ```

   - `a` attaches to the container.
   - `i` makes it interactive so you can use the terminal.

##### (optional) Remove the old container:

```bash
docker rm <container_id>
```

3. Start a new Ubuntu container:
   ```bash
   docker run -it ubuntu bash
   ```

   This will:

    - Pull the Ubuntu image (if not already downloaded).
    - Start a fresh container.
    - Drop you into the Bash shell of the Ubuntu container.

4. Verify you are in Ubuntu:
   ```bash
   cat /etc/os-release
   ```

- To exit the container's terminal: `exit`.
- To detach without stopping the container: `Ctrl + P`, `Ctrl + Q`.
- To stop the container: `docker stop <container_name_or_id>`.

<img src="https://github.com/akashdip2001/college-final-year-project/raw/main/img/colour_line.png">

### To re-enter an already running or stopped container, you can follow these steps:

1. **List all containers:**
   ```bash
   docker ps -a
   ```

2. **Attach to a running container:**
   ```bash
   docker attach <container_id_or_name>
   ```

3. **Start and attach to a stopped container:**
   ```bash
   docker start -ai <container_id_or_name>
   ```

4. **Open a new Bash shell inside a running container:**
   ```bash
   docker exec -it <container_id_or_name> bash
   ```
