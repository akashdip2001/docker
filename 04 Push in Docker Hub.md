## To push a Docker container to your Docker Hub repository

![Screenshot (684)](https://github.com/user-attachments/assets/ae7592de-a0a5-4668-aa39-5fec37cd15b6)

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

