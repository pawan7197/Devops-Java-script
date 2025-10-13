# 🚀 Advanced Angular Application Development and Deployment Across Two Virtual Machines (VMs)

## 🎯 Objective

This project demonstrates how to **develop, build, and deploy an Angular Calculator application** across **two Ubuntu Virtual Machines (VMs)**:

- **VM1 (Development VM):** Used to develop and build the Angular application.  
- **VM2 (Deployment VM):** Used to deploy the built Angular application using **Nginx**.

The goal is to ensure the Angular Calculator runs successfully when accessed via **VM2’s public IP**, with proper **Angular routing** and **Nginx configuration**.

---

## 🧩 Project Overview


✅ Develop an Angular Calculator application on VM1.  
✅ Build and prepare the application for production deployment.  
✅ Deploy the Angular app on VM2 using Nginx.  
✅ Configure Nginx for Single Page Application (SPA) routing.  
✅ Document every step (with screenshots, configurations, and resolutions).  
✅ Troubleshoot and verify successful deployment.

---

## 🖥️ Virtual Machines Setup

| VM | Role | Tools Installed | Purpose |
|----|------|------------------|----------|
| **VM1** | Development | Node.js, npm, Angular CLI | Build Angular App |
| **VM2** | Deployment | Nginx | Host and serve the built Angular App |

---

## 🪜 Step-by-Step Implementation

### **1️⃣ Setting Up VM1 (Development VM)**

#### 1.1: VM1 Configuration
```bash
sudo apt -y update
sudo apt -y upgrade
sudo hostnamectl set-hostname vm1-dev
```
1.2: Install Node.js, npm, and Angular CLI
```
sudo apt install nodejs npm -y
node -v
npm -v
sudo npm install -g @angular/cli
```
1.3: Clone the Repository
```
git clone https://github.com/Ai-TechNov/AngularCalculator.git
cd AngularCalculator
```
📸 Screenshot 1: Terminal output showing successful clone and directory structure.

1.4: Install Project Dependencies
```
npm install
```


1.5: Build the Angular Application
```
sudo ng build --prod
```
📸 Screenshot 3: Successful build showing the creation of the dist/ folder.

2️⃣ Setting Up VM2 (Deployment VM)
2.1: VM2 Configuration
```
sudo apt -y update
sudo apt -y upgrade
sudo hostnamectl set-hostname vm2-prod
```
2.2: Install Nginx
```
sudo apt install nginx -y
sudo systemctl status nginx
📸 Screenshot 4: Successful Nginx installation.


3️⃣ Transfer the Angular Application to VM2
3.1: Transfer Build Files from VM1 to VM2
On VM1, navigate to the Angular build directory:
```
cd dist/angularCalc
```
Transfer files using scp:

```
scp -r * username@<vm2-ip>:/var/www/html/
```
Replace:

username → VM2 username

```

<vm2-ip> → VM2 public IP address
```



3.2: Verify File Transfer on VM2
On VM2:

```
ls /var/www/html/
```

4️⃣ Configure Nginx on VM2
4.1: Edit Nginx Default Configuration
Open the default Nginx configuration file:

```
sudo nano /etc/nginx/sites-available/default
Replace the existing server block with:
```
```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    index index.html;

    server_name _;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

4.2: Restart Nginx
```
sudo systemctl restart nginx
```

5️⃣ Verify the Application
5.1: Access Application from Browser
```
Open your browser and visit:

http://<vm2-ip>
```

```
✅ The Angular Calculator should load successfully.
```


```
## Additional Notes##
Ensure both VMs are on the same network (for scp and deployment).

Allow HTTP (port 80) in VM2’s firewall or security group.

Keep your /etc/nginx/sites-available/default secure.

Use sudo nginx -t to validate config changes before restarting.

🧑‍💻 Author
PawanKumar Kothapalli
🎓  DevOps & Cloud Enthusiast
📍 Hyderabad, India
🌐 GitHub: https://github.com/PawanKumarKothapalli

🏁 Final Outcome
After successful completion:
✅ The Angular Calculator application runs seamlessly on VM2.
✅ It can be accessed via http://<vm2-public-ip>.
✅ Angular routing and Nginx configuration work correctly.
✅ Documentation contains all commands, configurations, and screenshots.









