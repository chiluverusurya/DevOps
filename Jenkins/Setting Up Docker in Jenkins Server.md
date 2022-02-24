# Setting Up Docker in Jenkins Server

You have to login as jenkins user before proceeding with below defined steps.

1. Install Docker

   ```sh
   curl -fsSL get.docker.com | /bin/bash
   ```

2. Add Jenkins user to docker group

   ```sh
   sudo usermod -aG docker jenkins
   ```

3. Restart Jenkins

   ```sh
   sudo systemctl restart jenkins
   ```
