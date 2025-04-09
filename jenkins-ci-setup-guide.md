# 🚀 Jenkins CI Setup Guide

A comprehensive guide to setting up Jenkins CI integration with GitHub.

![CI/CD Overview](./images/CICD_pipeline_overview.png)

---

## 🔗 Jenkins to GitHub Link

1. Click **New Item** in the left-side navigation bar.  
2. Enter a **Name** (e.g. `caleb-job-ci-test`).  
3. Select **Freestyle project**.  
   ![Project Creation](./images/project_creation.png)

4. Add a **Description** – make it meaningful.  
5. Tick **Discard old builds**:  
   - Set **Max number of builds to keep** = `3`.  
   ![Project Description](./images/project_description.png)

6. Tick **GitHub project**:  
   - Paste in the repository URL from your browser (ensure it ends with a `/`).  
   ![Project GitHub Link](./images/project_github_link.png)

7. Under **Source Code Management**:  
   - Select **Git**.  
   - Paste the **SSH clone link** from GitHub.  
   ![Adding Credentials](./images/adding_credentials.png)

   - Click **Add** underneath credentials:
     - **Domain**: Global  
     - **Kind**: SSH Username with private key  
       - **Scope**: Global  
       - **ID**: e.g. `tech503-caleb-jenkins-github-nodejs-key`  
       - **Description**: Clear and descriptive  
       - **Username**: Same as ID  
       ![Credentials Settings](./images/credentials_settings.png)
       - **Private Key**:  
         - Select **Enter directly**  
         - Paste your **private key**  
         - Click **Save**  
         ![Private Key Settings](./images/private_key_settings.png)

   - Select your newly added **Credential**.  
   - Under **Branches to build**:  
     - Change **Branch Specifier** to `*/dev`.  
     ![Branch Specifier](./images/branch_specifier.png)

8. Under **Build Triggers**:  
   - Tick **GitHub hook trigger for GITScm polling**  
   ![Build Trigger](./images/build_trigger_webhook.png)

9. Under **Build Environment**:  
   - Tick **Provide Node & npm bin/folder to PATH**  
   - Select **NodeJS Version 20**  
   ![Build Environment](./images/build_environment.png)

10. Under **Build Steps > Execute Shell**, add:
    ```bash
    ls
    cd app
    npm install
    npm test
    ```
    ![Build Steps](./images/build_steps.png)

11. Click **Save**.

> **Note:** To run the job manually, click **Build Now** in the left navigation bar.  
> To view logs, open the dropdown for the build and click **Console Output**.  
![Viewing Output](./images/viewing_console.png)

---

## 🔁 Linking Jobs

1. Go to **Dashboard > Select Job**.  
2. Click **Configure**.  
3. Scroll to **Post-build Actions**:  
   - Select **Build other projects**  
   - Enter the **job name** to trigger  
   - Tick **Build only if stable**  
   ![Linking Jobs](./images/linking_jobs.png)

---

## 🔐 Adding SSH Key to GitHub

1. Navigate to your GitHub **Repo > Settings > Deploy keys**  
   ![GitHub Deploy Keys](./images/github_deploy_keys.png)

2. Click **Add deploy key**  
3. Enter a **Name** for your key  
4. Paste your **public key** into the key field  
5. Tick **Allow write access**  
6. Click **Add key**  
   ![GitHub New Deploy Key](./images/github_add_deploy_key.png)

> ⚠️ **Important:** A GitHub SSH key can only be used with **one** repository.

---

## 📡 Setting up GitHub Webhook

1. Go to your repository on GitHub.  
2. Navigate to **Settings > Webhooks**  
   ![GitHub Webhooks](./images/github_webhooks.png)

3. Click **Add webhook**  
   - **Payload URL**: Enter your Jenkins URL followed by `/github-webhook/`  
     Example:  
     ```
     http://jenkins-ip-here:8080/github-webhook/
     ```
   - **SSL verification**: Tick **Disable**  
   ![GitHub Webhook Settings](./images/github_webhook_settings.png)

4. Click **Add webhook**

---
