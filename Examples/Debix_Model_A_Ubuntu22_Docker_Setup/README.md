### Installing and Using Docker on DEBIX Model A (Ubuntu 22.04)  

🧱 Step 1: Update System Software Sources  
```shell  
sudo apt update  
```  
Ensure the system is up-to-date to avoid dependency issues during installation.  

🐳 Step 2: Install Docker  
```shell  
sudo apt install docker.io -y  
```  
📦 `docker.io` is the stable Docker version in Ubuntu's official repository.  

🔧 Step 3: Start Docker Service  
```shell  
sudo systemctl start docker  
```  

🔁 Step 4: Enable Docker Autostart  
```shell  
sudo systemctl enable docker  
```  
Docker will automatically start after every system reboot.  

🧪 Step 5: Verify Docker Installation  
```shell  
docker --version  
```  
Example output:  
```shell  
Docker version 24.x.x, build abcdefg  
```  

🚀 Step 6: Run Your First Container  
```shell  
sudo docker run hello-world  
```  
✅ If installed correctly, you'll see:  
```shell  
Hello from Docker!  
This message shows that your installation appears to be working correctly.  
```