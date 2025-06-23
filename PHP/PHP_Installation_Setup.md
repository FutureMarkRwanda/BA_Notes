# PHP Installation and Setup

## Summary

This topic covers the installation and configuration of PHP using XAMPP, a popular AMP (Apache, MySQL, PHP) stack for running PHP applications on Windows. It includes steps for setup and troubleshooting common issues.

- **XAMPP Installation**: Installing XAMPP on Windows for PHP development.
- **Verification and Troubleshooting**: Ensuring PHP runs correctly and resolving issues.

---

## XAMPP Installation

XAMPP is a cross-platform AMP stack that includes PHP, Apache, MySQL, and additional tools like FileZilla and OpenSSL, enabling developers to run PHP applications locally.

**Steps to Install XAMPP on Windows**:
1. Download XAMPP from https://www.apachefriends.org/download.html, selecting the appropriate version for Windows.
2. Run the installer, allow system changes, and click **Next**.
3. Select components (Apache, MySQL, PHP) and click **Next**.
4. Choose an installation directory (e.g., `C:\xampp`) and click **Next**.
5. Proceed through prompts, clicking **Next** to install.
6. Click **Finish** and select your preferred language.
7. Open XAMPP Control Panel, start Apache and MySQL.
8. Verify by navigating to `http://localhost` in a browser to see the XAMPP dashboard.

**Example**:
- A developer downloads XAMPP 8.2, installs it in `C:\xampp`, and confirms Apache/MySQL are running via the Control Panel.
- Scenario: A student sets up XAMPP to test PHP scripts locally for a web development course.

---

## Verification and Troubleshooting

After installation, verify XAMPP is running correctly and troubleshoot common setup issues to ensure PHP scripts execute properly.

**Verification**:
- Access `http://localhost` to confirm Apache is running.
- Create a test PHP file (e.g., `test.php`) in `C:\xampp\htdocs`:
```php
<?php
phpinfo();
?>
```
- Navigate to `http://localhost/test.php` to view PHP configuration details.
- Start MySQL in XAMPP Control Panel and access `http://localhost/phpmyadmin` to verify database functionality.

**Troubleshooting Tips**:
- **Apache Won’t Start**: Check for port conflicts (80/443) using `netstat -aon`. Edit `C:\xampp\apache\conf\httpd.conf` to change ports (e.g., 8080) or stop conflicting apps (e.g., Skype).
- **MySQL Fails**: Ensure no other MySQL instances are running. Check `C:\xampp\mysql\data` for errors.
- **Access Denied**: Verify `htdocs` has write permissions for PHP file creation.
- **Blank Page**: Confirm PHP module is enabled in XAMPP Control Panel.

**Example**:
- A developer sees a blank page at `http://localhost/test.php`, checks Apache status, and restarts it to resolve.
- Scenario: A beginner fixes a port conflict by changing Apache’s port to 8080, allowing localhost access for PHP testing.