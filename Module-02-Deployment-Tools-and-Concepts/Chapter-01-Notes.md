# Week 2, Session 1

**Topic:** Containerization (Podman), Docker Files, and Networking

---

## Concept Explanations

### 1. The Need for Containerization
When we write code, it depends on specific OS versions, Python libraries, and system tools. "It works on my machine" is a common problem.
* **Solution:** Packaging everything (Code + OS + Libraries) into a single "Image".
* **Image vs. Container:**
    * **Image:** A static file (like a snapshot) containing the application and its dependencies.
    * **Container (or Pod):** A running instance of an image. It is an isolated environment (like a lightweight virtual machine) that runs on your RAM.

### 2. Podman vs. Docker
We use **Podman** in this course. It is an open-source alternative to Docker.
* **Key Difference:** Podman is "daemonless" and doesn't require root privileges (safer), whereas Docker runs as a background daemon with root access.
* **Compatibility:** Most Docker commands work in Podman (e.g., `docker run` -> `podman run`).

### 3. Core Container Concepts
* **Pulling:** Downloading an image from a registry (like Docker Hub or Quay.io).
* **Port Forwarding (`-p`):** Containers are isolated. To access a server running inside a container (e.g., on port 8888) from our local browser, we must "map" a local port to the container's port.
* **Volumes (`-v`):** If a container is deleted, its data is lost. We use volumes to map a folder on our local machine to a folder inside the container, ensuring data persistence.
* **Networking:** By default, containers cannot talk to each other. We create a dedicated **Network** so that different containers (e.g., a Jupyter Lab container and an Ollama container) can communicate.

---

## Examples and Code Snippets

### 1. Basic Podman Commands
Run these in your WSL/Ubuntu terminal:

```bash
# Pull an image (e.g., a small Jupyter Lab image)
podman pull docker.io/jupyter/base-notebook

# Run a container (Interactive mode)
# -it: Interactive terminal
# --rm: Remove container after exit
podman run -it --rm docker.io/jupyter/base-notebook

# Run in Detached mode (Background) with Port Mapping
# -d: Detached
# -p 8888:8888 : Map local port 8888 to container port 8888
# --name: Give it a friendly name
podman run -d -p 8888:8888 --name my_notebook docker.io/jupyter/base-notebook

# List running containers
podman ps

# Stop and Remove
podman stop my_notebook
podman rm my_notebook
```
2. Data Persistence (Volumes)
Mapping a local folder (~/project) to the container's work directory (/home/jovyan/work):

```bash
# Create a local directory first
mkdir ~/project
chmod 777 ~/project

# Run with Volume mapping (-v)
podman run -d \
  -p 8888:8888 \
  -v ~/project:/home/jovyan/work \
  --name notebook_with_data \
  docker.io/jupyter/base-notebook
```

3. Running Local AI (Ollama)
We used a lightweight Alpine Linux image to run Ollama and the Gemma:2b model.

```bash
# Run Ollama container
# Map port 11434 (Standard Ollama port)
# Mount a volume to save downloaded models
podman run -d \
  -p 11434:11434 \
  -v ollama_data:/root/.ollama \
  --name ollama_server \
  docker.io/ollama/ollama

# Execute a command INSIDE the running container to download a model
podman exec -it ollama_server ollama run gemma:2b
```

4. Container Networking
Connecting the Jupyter container to the Ollama container so they can talk.

```bash
# 1. Create a network
podman network create ai_network

# 2. Run Ollama on this network
podman run -d --network ai_network --name ollama_net ... (rest of args)

# 3. Run Jupyter on the SAME network
podman run -d --network ai_network --name jupyter_net ... (rest of args)

# Now, inside Jupyter, you can access Ollama using the hostname "ollama_net" instead of "localhost"
```
