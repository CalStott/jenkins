# Jenkins CI Setup Guide

### Create Your First Job

1. Click **New Item** in the left-side navigation bar.  
2. Enter a **Name** (e.g. `caleb-first-job`).  
3. Select **Freestyle project**.  
4. Add a **Description** – make it meaningful.  
5. Tick **Discard old builds**:  
   - Set **Max number of builds to keep** = `3`.  
6. Under **Build Steps**, click **Add build step > Execute shell**.  
7. Click **Save**.  
8. On the left sidebar, click **Build Now**.  
9. After the build runs, click the dropdown > **Console Output**.

---

### 🔗 Linking Jobs

1. Go to **Dashboard > Select Job**.  
2. Click **Configure**.  
3. Scroll to **Post-build Actions**:  
   - Select **Build other projects**.  
   - Type in the job to trigger.  
   - Tick **Build only if stable**.

---

## 🔐 SSH Key on GitHub

1. Go to your GitHub **Repo > Settings > Deploy keys**.  
2. Click **Add new key**.  
3. Give your key a **Name**.  
4. Paste the **public key** into the key box.  
5. Tick **Allow write access**.  
6. Click **Add key**.

> ⚠️ **Note**: A GitHub SSH key can only be used for **one** repository.

---

## 🔗 Jenkins to GitHub Link

1. Create a **New Item**.  
2. Tick **Discard old builds** and set **Max # = 3**.  
3. Tick **GitHub project**:  
   - Paste in the URL from your browser (ensure it ends with a `/`).  
4. Under **Source Code Management**:  
   - Tick **Git**.  
   - Paste the **SSH clone link** from GitHub.  
   - Click **Add** next to credentials:  
     - **Domain**: Global  
     - **Kind**: SSH Username with **private** key  
       - **Scope**: Global  
       - **ID**: e.g. `tech503-caleb-jenkins-github-nodejs-key`  
       - **Description**: Clear and descriptive  
       - **Username**: Same as ID  
       - **Private Key**:  
         - Tick **Enter directly**  
         - Paste the **private key** (no passphrase)  
         - Click **Save**  
   - Select your newly added **Credential**.  
   - Under **Branches to build**:  
     - Change **Branch Specifier** to `*/main`.

5. **Build Environment**:  
   - Tick **Provide Node & npm bin/folder to PATH**.  
   - Choose **NodeJS Version 20**.

6. **Build Steps > Execute Shell**:
   ```bash
   ls
   cd app
   npm install
   npm test
   ```

7. Click **Save**.

