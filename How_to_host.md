# Launch EC2 Instance

### 
Login into AWS Console -> Go to the AWS EC2 Console and sign in.

#### Step 1: Choose an Amazon Machine Image (AMI) -> Amazon Linux AMI

#### Step 2: Choose an Instance Type -> Select t2.micro (eligible for free tier).

#### Step 3: Configure Instance Details -> Keep all default settings.

#### Step 4: Add Storage -> Use the default 8 GiB (or modify as needed).

#### Step 5: Configure Security Group -> Create a new security group or use an existing one.

#### Step 6: Add the following inbound rules:

        HTTP (80) → Anywhere (0.0.0.0/0, ::/0)

        HTTPS (443) → Anywhere (0.0.0.0/0, ::/0)

        SSH (22) → Your IP (for security, not Anywhere)
#### Step 7: Review and Launch

#### Step 8: Click Launch Instance -> Using EC2 Instance Connect.


###  
# Follow these steps in the CLI



### 1. Update Your System:

```bash
sudo yum update -y
```

### 2. Install Nginx:

```bash
sudo yum install nginx -y
```

### 3. Start Nginx:

```bash
sudo systemctl start nginx
```

### 4. Enable Nginx to Start on Boot:

```bash
sudo systemctl enable nginx
```

### 5. Create a Dummy `index.html`:

Create a file named `index.html` with the following content:

```bash
echo '<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>NGINX Server</title></head><body><div id="app"><h1>Guide to host NGINX Server</h1><p>This is a dummy single-page application for testing.</p></div></body></html>' > index.html
```

### 6. Copy `index.html` to Nginx's Default Directory:

```bash
sudo cp index.html /usr/share/nginx/html
```

### 7. Configure Nginx:

Edit the Nginx configuration file:

```bash
sudo nano /etc/nginx/nginx.conf
```

Inside the `server` block, update the `location /` block to point to your SPA's build directory:

```nginx
server {
    listen       80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html;
        try_files $uri $uri/ /index.html;
    }
}
```

### 8. Restart Nginx:

```bash
sudo systemctl restart nginx
```
