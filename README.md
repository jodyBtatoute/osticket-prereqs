<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

Here’s a **step-by-step guide** to installing **osTicket**, a popular open-source support ticketing system.

---

## 🧰 **Prerequisites**

Before installation, make sure your server meets the following requirements:

### 1. Server Requirements

* **Web Server:** Apache or Nginx
* **PHP:** 8.0–8.2 (PHP 8.3 not fully supported yet)
* **Database:** MySQL 5.5+ or MariaDB 10+
* **PHP Extensions:**

  ```
  mysqli
  gd
  gettext
  imap
  xml
  json
  mbstring
  phar
  fileinfo
  intl
  zip
  ```

### 2. Software Tools

* A web browser
* FTP/SFTP or direct shell access
* A text editor (e.g., Notepad++, VS Code)

---

## ⚙️ **Installation Steps**

### **Step 1: Download osTicket**

1. Visit the official site: [https://osticket.com/download/](https://osticket.com/download/)
2. Download the latest stable release (e.g., `osTicket-v1.18.x.zip`).

---

### **Step 2: Upload Files to Your Web Server**

1. Extract the `.zip` file locally.
2. Upload the contents of the **“upload”** folder to your web root directory, e.g.:

   ```
   /var/www/html/support/
   ```
3. Rename the file:

   ```
   ost-sampleconfig.php → ost-config.php
   ```

   This file is located in the `include/` directory:

   ```
   include/ost-sampleconfig.php
   ```

---

### **Step 3: Set Permissions**

Set writable permissions for the configuration file and the following directories:

```bash
chmod 0666 include/ost-config.php
chmod -R 0775 include/
chmod -R 0775 attachments/
chmod -R 0775 setup/
```

---

### **Step 4: Create a MySQL Database**

1. Log in to MySQL:

   ```bash
   mysql -u root -p
   ```
2. Create a database and user:

   ```sql
   CREATE DATABASE osticket;
   CREATE USER 'ostuser'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON osticket.* TO 'ostuser'@'localhost';
   FLUSH PRIVILEGES;
   ```
3. Exit MySQL:

   ```bash
   exit
   ```

---

### **Step 5: Run the Web Installer**

1. Open your web browser and navigate to:

   ```
   http://your-domain.com/support/setup/
   ```

2. Follow the on-screen instructions:

   * Enter **System Settings** (site name, email, etc.)
   * Enter **Admin User** details (name, email, password)
   * Enter **Database Settings** (database name, username, password)

3. Click **Install Now**.

---

### **Step 6: Finalize Installation**

1. After installation completes successfully:

   * Delete the **setup/** folder for security:

     ```bash
     rm -rf setup/
     ```
   * Set your config file to read-only:

     ```bash
     chmod 0644 include/ost-config.php
     ```

---

### **Step 7: Access osTicket**

* **Admin Panel:**

  ```
  http://your-domain.com/support/scp
  ```
* **Client Portal:**

  ```
  http://your-domain.com/support/
  ```

Use the admin credentials you set during installation to log in.

---

## ✅ **Post-Installation Recommendations**

* Configure email piping or IMAP for ticket creation via email.
* Set up cron jobs for auto tasks:

  ```bash
  */5 * * * * /usr/bin/php /var/www/html/support/api/cron.php
  ```
* Backup the database and configuration files regularly.

---

Would you like me to give you the **Windows XAMPP-based installation** steps or **Linux (Ubuntu)** specific commands?
