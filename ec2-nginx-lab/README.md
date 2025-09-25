# EC2 + NGINX Lab

## What I built
- Amazon Linux 2023 (t3.micro) in **us-west-2**
- Key pair: `ardy-mac-ed25519`
- Security Group: SSH from My IP, HTTP from Anywhere

## Steps
1. Launch EC2 (public IP enabled) and select the key pair above.
2. Connect:
   ```bash
   ssh -i ~/.ssh/id_ed25519 ec2-user@<public_ip>
3. Install & start NGINX:
   sudo dnf update -y
   sudo dnf install -y nginx
   sudo systemctl enable --now nginx
   echo "Hello from Ardy 🚀" | sudo tee /usr/share/nginx/html/index.html
4. Verify in browser: http://<PUBLIC_IP>
5. Cleanup: Terminate instance; delete any unattached EBS volumes.

##Lessons Learned
-Key pair: AWS stores the public key on the instance; my private key stays on my Mac.
-Session Manager = browser shell, no SSH key, needs IAM role AmazonSSMManagedInstanceCore.
-Keep SSH restricted to My IP; only HTTP/HTTPS open to the world.
