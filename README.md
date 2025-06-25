My Virtual Server Lab Journey 🚀

This document outlines the complete journey of setting up a virtual server environment on an Ubuntu Linux machine. It details the steps taken, the challenges faced, and the solutions implemented to create a fully functional, two-way connected development lab.
🛠️ Tools & Technologies Used

    Host OS: Ubuntu Desktop

    Virtualization: VMware Workstation Pro

    Server OS: Ubuntu Server 24.04.2 LTS

    Core Protocol: SSH (Secure Shell)

    Web Server: Nginx

    Terminal Editors: nano

Phase 1: Setting up the Foundation 🏗️

The first step was to create the environment where our server would live.

    ✅ Installed VMware Workstation: Navigated the Broadcom portal to download the correct .bundle installer for Linux.

    ✅ Prepared the Installer: Used the terminal to make the installer executable (chmod +x ...) and run it with superuser privileges (sudo ./...).

    🔴 Challenge: A No such file or directory error occurred when trying to run chmod.

    💡 Solution: We carefully compared the typed filename with the actual filename from the ls command and found a typo in the build number. Correcting the filename fixed the issue.

Phase 2: Building the Server 🖥️

With VMware ready, we created the server itself.

    ✅ Downloaded Ubuntu Server: Acquired the official Ubuntu Server 24.04.2 LTS .iso image.

    ✅ Created a New Virtual Machine: Used the VMware wizard to create a new VM, pointing to the downloaded .iso file as the virtual CD-ROM.

    ✅ Completed the OS Installation: Successfully navigated the Ubuntu Server text-based installer, configuring the network, storage, and creating the sharma1 user.

Phase 3: Establishing Remote Connections 🌐

This was the most challenging and rewarding phase, focused on getting the physical laptop and the virtual server to communicate.
Connection 1: Laptop → Server

    🔴 Challenge: The first SSH attempt (ssh sharma1@192.168.218.128) resulted in a Connection refused error.

    💡 Solution: We diagnosed the problem on the server.

        sudo systemctl status ssh showed Unit ssh.service could not be found., proving the SSH server was not installed.

        We fixed this by running sudo apt install openssh-server on the server.

        We then started and enabled the service with sudo systemctl start ssh and sudo systemctl enable ssh.

    🎉 Result: A successful SSH connection from the laptop to the server!

Connection 2: Server → Laptop

    ✅ Preparation: To allow incoming connections, we installed the SSH server on the host laptop with sudo apt install openssh-server.

    🔴 Challenge: The second SSH attempt (ssh sharmake@192.168.218.1) resulted in a Permission denied (publickey,password) error, even with the correct password.

    💡 Solution: We identified that the laptop's SSH server configuration was not allowing password-based logins by default.

        We edited the configuration file: sudo nano /etc/ssh/sshd_config.

        We explicitly enabled password logins by adding the line PasswordAuthentication yes to the file.

        We applied the changes by restarting the service: sudo systemctl restart ssh.

    🎉 Result: A successful SSH connection from the server back to the laptop, achieving full two-way communication!

🧠 Key Skills Learned

    Virtualization: How to use a hypervisor (VMware) to create and manage virtual machines.

    System Administration: Installing and configuring a Linux server operating system from scratch.

    Networking: Understanding the difference between private and public IPs, and how virtual networks operate.

    Troubleshooting: Methodically diagnosing and solving common connection errors like Connection refused and Permission denied.

    Command Line Proficiency: Using commands like ip a, systemctl, apt, chmod, and nano to manage and configure Linux systems.

    SSH Protocol: How to securely connect to remote machines and the importance of server configuration files (sshd_config).

This project was a complete success and built a foundational, professional-grade development environment. Well done!
