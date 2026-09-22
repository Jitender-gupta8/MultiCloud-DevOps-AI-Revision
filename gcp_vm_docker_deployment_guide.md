# GCP VM Setup & Docker Container Deployment Guide

This guide details the complete process of launching an Ubuntu Virtual Machine on Google Cloud Platform (GCP), installing Docker, running a web application container (`win11react`), and configuring firewall settings for internet access.

---

## 📌 Summary of Steps

1. **Create a VM Instance:** Spin up an Ubuntu 24.04 LTS instance on Google Compute Engine.
2. **Connect via SSH:** Access the server terminal using GCP's built-in SSH-in-browser.
3. **Install Docker:** Update package repositories and install the `docker.io` package.
4. **Run Container:** Pull and launch the `blueedge/win11react` Docker container mapped to port `3000`.
5. **Configure GCP Firewall:** Open inbound TCP port `3000` to make the application publicly accessible.
6. **Access Application:** Open `http://<YOUR_PUBLIC_IP>:3000` in a browser.

---

## Step 1: Create a VM Instance on GCP

1. Log in to the [Google Cloud Console](https://console.cloud.google.com/).
2. Navigate to **Compute Engine** > **VM instances**.
3. Click **Create Instance**.
4. Configure the instance:
   * **Name:** `jitender-22sept` (or your preferred name)
   * **Region/Zone:** `us-central1-c`
   * **Machine Configuration:** Select a standard machine type (e.g., `e2-medium`).
   * **Boot Disk:** Change OS to **Ubuntu**, version **Ubuntu 24.04 LTS**.
   * **Firewall:** Check **Allow HTTP traffic** and **Allow HTTPS traffic**.
5. Click **Create**.

---

## Step 2: Connect via SSH and Switch to Root

1. In the **VM instances** list, find your running instance (`jitender-22sept`).
2. Click the **SSH** button next to your instance to open the web-based terminal.
3. Gain elevated (root) privileges:
   ```bash
   sudo -i
   ```

---

## Step 3: Install Docker on the VM

1. Update the local package package database:
   ```bash
   apt update
   ```

2. Install Docker:
   ```bash
   apt install docker.io -y
   ```

3. Verify Docker installation and check the installed version:
   ```bash
   docker -v
   ```
   *Expected Output:* `Docker version 29.1.3, build ...` (or similar version).

---

## Step 4: Run the Docker Container

Run the `blueedge/win11react` image in detached mode, configuring it to automatically restart unless explicitly stopped:

```bash
docker run -d --restart unless-stopped --name win11react -p 3000:3000 blueedge/win11react:latest
```

* **`-d`**: Runs container in background (detached mode).
* **`--restart unless-stopped`**: Automatically restarts container if host reboots.
* **`--name win11react`**: Assigns a container name.
* **`-p 3000:3000`**: Maps host port 3000 to container port 3000.

Verify the container is active and running:
```bash
docker ps
```

---

## Step 5: Configure GCP Firewall for Port 3000

By default, GCP blocks incoming traffic on non-standard web ports like `3000`. You must open port `3000` in the GCP firewall settings.

### Option A: Using `gcloud` CLI (Fastest)
Run this command directly in your SSH terminal:
```bash
gcloud compute firewall-rules create allow-port-3000 \
    --allow=tcp:3000 \
    --description="Allow incoming traffic on port 3000" \
    --direction=INGRESS
```

### Option B: Via Google Cloud Console UI
1. Go to **VPC network** > **Firewall** in GCP Console.
2. Click **Create Firewall Rule**.
3. Set the following parameters:
   * **Name:** `allow-port-3000`
   * **Targets:** `All instances in the network`
   * **Source IPv4 ranges:** `0.0.0.0/0`
   * **Protocols and ports:** Check `Specified protocols and ports`, choose `tcp`, and set port to `3000`.
4. Click **Create**.

---

## Step 6: Verify External Access

1. Find your VM's **External IP** (e.g., `35.226.219.206`).
2. Open a web browser and navigate to:
   ```text
   http://<YOUR_PUBLIC_IP>:3000
   ```
   *Example:* `http://35.226.219.206:3000`
3. You should see the **Win11 in React** desktop user interface running live.