# Raspberry Pi Streaming Service

This repository contains a Python script for setting up a real-time video streaming server using the Raspberry Pi Camera Module. The stream is served over HTTP and can be accessed via a web browser with the assistance of the Nginx web server.

## **Prerequisites**

- Raspberry Pi with Camera Module.
- Nginx web server installed and configured.
- Python 3.x
- Required Python libraries: `picamera2`, `cv2`, `io`, `logging`, `socketserver`, `datetime`, `http.server`, `threading`.

## **Installation & Configuration**

### **1. Nginx Configuration**

- Navigate to your Nginx configuration, typically found at `/etc/nginx/sites-available/default`.

- Add the following configuration to handle the streaming:
  
```nginx
location / {
    proxy_pass http://localhost:8080;
    proxy_redirect off;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

### **2. SSL Configuration Using Let's Encrypt**

- Install `certbot`:

```bash
sudo apt-get install certbot python3-certbot-nginx
```

- Obtain and Install a certificate:

```bash
sudo certbot --nginx
```

- Follow the on-screen prompts from Certbot to enable HTTPS.

- Save and restart Nginx:

```bash
sudo systemctl restart nginx
```

### **3. Script Configuration**

- Install the necessary libraries:

```bash
pip3 install picamera2 cv2
```

- Clone this repository or download `cam-streamer.py`.

- Provide execution permissions:

```bash
chmod +x cam-streamer.py
```

- Run the script:

```bash
./cam-streamer.py
```

The script initiates an HTTP server on port `8080` and starts serving the video feed.

## **Usage**

Upon successful configuration, access the stream via:

```
https://your_raspberry_pi_ip_address/
```

The video stream will display with an accompanying timestamp on each frame.
```

Please replace `your_raspberry_pi_ip_address` with your actual Raspberry Pi's IP address when accessing the stream.
