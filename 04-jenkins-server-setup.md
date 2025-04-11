# Jenkins Server Guide

## Follow VPC Deployment Guide (put link here to guide)

## Creating a Jenkins EC2 Instance

1. Launch New Instance from EC2 Dashboard
2. Name e.g tech503-caleb-jenkins-server
3. Images
   1. Quick Start
   2. Select Ubuntu 22.04
4. Instance Type
   1. t2.micro or t3.micro
5. Key Pair
   1. Select your SSH key
6. Network Settings
   1. Edit
   2. Select your VPC from the dropdown
   3. Select your Subnet from the dropdown
   4. Auto-assign public IP - Enable
   5. Firewall
      1. Create Security Group
      2. Name e.g. tech503-caleb-jenkins-sg-vpc
      3. Description - same as name
      4. Rules - Ports 22 - SSH, 80 - HTTP, 8080 - Jenkins
7. Launch instance

## Installing Dependencies

1. Connect to your EC2 instance via SSH
2. Install Jenkins
   1. Run these commands in the terminal
      ```bash
        # This downloads the GPG key (used to verify package authenticity) from the specified URL and saves it to the specified location
        sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
        https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

        # Adds a new source for APT (the package manager) by creating a .list file
        # Tells APT where to fetch Jenkins packages, to use the GPG key and saves the information
        echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
        https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
        /etc/apt/sources.list.d/jenkins.list > /dev/null
        
        # Updates the package index and installs Jenkins
        sudo apt-get update
        sudo apt-get install jenkins -y
      ``` 

3. Install Java
   1. Run these commands in the terminal
    ```bash
    # Installs OpenJDK 17
    sudo apt install fontconfig openjdk-17-jre -y
    
    # Checks the installation
    java -version
    ```  
   2. You should see this output in the terminal

4. Start Jenkins
   1. Run these commands in the terminal
    ```bash
    sudo systemctl enable jenkins
    sudo systemctl start jenkins
    ```
   2. Optional: Check the status of Jenkins - `sudo systemctl status jenkins`

5.  Go to your EC2 instance public IP address
    1.  To fetch the administrator password, run this command
        ```bash
        sudo cat /var/lib/jenkins/secrets/initialAdminPassword
        ```
    2. Paste the output into the website

6. Customise Jenkins
   1. Install suggested plugins
   2. Create a user or skip and continue as admin
   3. Dashboard > Manage Jenkins > Plugins
      1. Available Plugins
         1. Install NodeJS plugin
         2. Dashboard > Manage Jenkins > Tools
            1. NodeJS > Add NodeJS
            2. Name e.g. NodeJS 20.0.0
            3. Save
   4. Dashboard > Manage Jenkins > Security
      1. Git Host Key Verification Configuration
         1. Select no verification from the dropdown
         2. Select Manually provided keys
            1. Paste this into the textbox - it is GitHub's public SSH key fingerprint
                ```bash
                github.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOMqqnkVzrm0SdG6UOoqKLsabgH5C9okWi0dh2l9GKJl
                ``` 

7. Create your pipeline (link to CI setup)
   1. Create Job to test the code base
   2. Create Job to merge the code into main
   3. Create job to take the new code, access the app instance and run the app
8. 

Build your own Jenkins server

- Use Ubuntu 22.04 LTS
- Size:
  - Use t2.micro or t3.micro size
- Launch it in your own VPC (public subnet)
- Reminder --> Security Group Rules?
- Many resources online on how to setup Jenkins in Ubuntu
- Recommend using plugins for Git and NodeJs (as we did on our shared servers)
