# SatTask
Got it! Let me simplify everything for you and provide a step-by-step guide specifically for Ubuntu using the terminal. I'll make it super easy to follow, even if you're new to this. 😊

---

### **Step 1: Install Required Tools**
Open your terminal and run the following commands to install Git, Maven, Java, and Tomcat:

```bash
sudo apt update
sudo apt install git maven default-jdk
```

---

### **Step 2: Download and Set Up Tomcat**
1. Download Apache Tomcat:
   ```bash
   wget https://downloads.apache.org/tomcat/tomcat-10/v10.1.7/bin/apache-tomcat-10.1.7.tar.gz
   ```
   (You can replace the URL with the latest version from the [Tomcat website](https://tomcat.apache.org/download-10.cgi).)

2. Extract the downloaded file:
   ```bash
   tar -xvzf apache-tomcat-10.1.7.tar.gz
   ```

3. Move the extracted folder to `/opt/tomcat`:
   ```bash
   sudo mv apache-tomcat-10.1.7 /opt/tomcat
   ```

4. Set environment variables for Tomcat:
   Open the `~/.bashrc` file in a text editor:
   ```bash
   nano ~/.bashrc
   ```
   Add the following lines at the end of the file:
   ```bash
   export CATALINA_HOME=/opt/tomcat
   export PATH=$PATH:$CATALINA_HOME/bin
   ```
   Save the file and reload the shell:
   ```bash
   source ~/.bashrc
   ```

---

### **Step 3: Write the Shell Script**
Now, let's create a shell script to automate the deployment process.

1. Create a file named `deploy.sh`:
   ```bash
   nano deploy.sh
   ```

2. Add the following content to the file:
   ```bash
   #!/bin/bash

   # Input: Git repository URL
   read -p "Enter Git repository URL: " repo_url

   # Step 1: Clone the Git repository
   echo "Cloning the repository..."
   git clone "$repo_url" app

   # Step 2: Navigate into the cloned repository
   cd app

   # Step 3: Build the Maven project
   echo "Building the Maven project..."
   mvn clean package

   # Step 4: Copy the generated WAR file to Tomcat's webapps directory
   echo "Deploying the WAR file to Tomcat..."
   cp target/*.war $CATALINA_HOME/webapps/

   # Step 5: Start Tomcat
   echo "Starting Tomcat..."
   $CATALINA_HOME/bin/catalina.sh start

   echo "Deployment completed! Tomcat is running."
   ```

3. Save the file and exit the editor:
   - Press `CTRL + X`, then `Y`, and then `Enter`.

4. Make the script executable:
   ```bash
   chmod +x deploy.sh
   ```

---

### **Step 4: Run the Script**
Execute the script by running:
```bash
./deploy.sh
```

When prompted, enter the Git repository URL of your Maven-based Java application.

---

### **Step 5: Access Your Application**
Once the script completes, your application will be deployed on Tomcat. You can access it in your browser at:
```
http://localhost:8080/your-app-name
```
Replace `your-app-name` with the name of the WAR file (without the `.war` extension).

---

### **Step 6: Stop Tomcat (Optional)**
If you want to stop Tomcat, you can use:
```bash
$CATALINA_HOME/bin/catalina.sh stop
```

---

### **Summary of Commands**
Here’s a quick summary of all the commands you need to run:

1. Install tools:
   ```bash
   sudo apt update
   sudo apt install git maven default-jdk
   ```

2. Download and set up Tomcat:
   ```bash
   wget https://downloads.apache.org/tomcat/tomcat-10/v10.1.7/bin/apache-tomcat-10.1.7.tar.gz
   tar -xvzf apache-tomcat-10.1.7.tar.gz
   sudo mv apache-tomcat-10.1.7 /opt/tomcat
   nano ~/.bashrc
   ```
   Add these lines to `~/.bashrc`:
   ```bash
   export CATALINA_HOME=/opt/tomcat
   export PATH=$PATH:$CATALINA_HOME/bin
   ```
   Save and reload:
   ```bash
   source ~/.bashrc
   ```

3. Create and run the script:
   ```bash
   nano deploy.sh
   ```
   Paste the script content, save, and make it executable:
   ```bash
   chmod +x deploy.sh
   ./deploy.sh
   ```

4. Access your app:
   ```
   http://localhost:8080/your-app-name
   ```

---

That's it! You’ve successfully deployed a Maven-based Java application on Tomcat using a shell script in Ubuntu. Let me know if you have any questions or run into any issues! 😄
