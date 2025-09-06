# Docker_installation_for_ARM
you’re on **Ubuntu for Raspberry Pi** (`aarch64` architecture) and want a **document** explaining how to install the latest Docker and Docker Compose.

Here’s a clean, ready-to-use **installation document** you can keep.

---

# **Installing Docker & Docker Compose on Raspberry Pi (Ubuntu aarch64)**

## **Overview**

This guide installs the **latest version** of Docker Engine and Docker Compose on a Raspberry Pi running **Ubuntu ARM64 (aarch64)**.
It ensures both tools are ARM-compatible and configured for everyday use.

---

## **1. System Update**

Update all existing packages:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## **2. Install Prerequisites**

Docker requires some system dependencies:

```bash
sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
```

---

## **3. Add Docker’s Official GPG Key**

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
```

---

## **4. Add the Docker APT Repository**

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## **5. Install Latest Docker Engine**

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```

---

## **6. Enable and Start Docker**

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

---

## **7. Install Docker Compose (Plugin)**

Docker Compose is now a CLI plugin.
Run:

```bash
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins

curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-aarch64 \
  -o $DOCKER_CONFIG/cli-plugins/docker-compose

chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
```

---

## **8. Verify Installation**

```bash
docker --version
docker compose version
```

Expected output example:

```
Docker version 27.x.x, build XXXXXXX
Docker Compose version v2.x.x
```

---

## **9. Run Docker Without `sudo` (Optional)**

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## **10. Test With Hello World**

```bash
docker run hello-world
```

If successful, you’ll see:

> Hello from Docker!

---

**Notes:**

* Architecture: This guide uses `aarch64` binaries (64-bit ARM).
* OS: Tested on **Ubuntu 22.04+ for Raspberry Pi**.
* To upgrade Docker/Compose in the future:

  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

---

## All Commands
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
sudo systemctl enable docker
sudo systemctl start docker
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins

curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-aarch64 \
  -o $DOCKER_CONFIG/cli-plugins/docker-compose

chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
sudo usermod -aG docker $USER
newgrp docker
```
