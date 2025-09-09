# devops-journey🚀

## 📌 Day 1: Introduction to DevOps

### 🔹 What is DevOps?
DevOps is a set of practices, tools, and a cultural mindset that combines software development (Dev) and IT operations (Ops).  
It focuses on collaboration, automation, and continuous delivery to deliver high-quality software faster.

### 🔹 Why DevOps is Needed
- Breaks the silos between developers and operations.
- Reduces manual deployment errors.
- Speeds up release cycles.
- Provides faster feedback and more reliable systems.

### 🔹 Benefits of DevOps
- **Speed:** Faster feature delivery.
- **Quality:** Automated testing reduces bugs.
- **Reliability:** Continuous monitoring improves stability.
- **Collaboration:** Better teamwork between Dev and Ops.
- **Scalability:** Infrastructure as Code makes scaling easier.

### 🔹 Key Concepts
- **Collaboration** – Dev + Ops working together.
- **Automation** – Automating builds, tests, deployments, and infrastructure.
- **CI/CD** – Continuous Integration & Continuous Delivery for faster releases.
- **IaC** – Infrastructure managed as code (e.g., Terraform, Ansible).
- **Monitoring** – Tracking system health (e.g., Prometheus, Grafana).

---

✅ This repo will track my **30-day DevOps learning journey** with notes, examples, and projects.

## 📌 Day 4: Linux Basics

### 🔹 Linux File System
- Linux uses a hierarchical directory structure:
  - `/` → root directory  
  - `/home` → user directories  
  - `/etc` → configuration files  
  - `/var` → logs and temporary files  
  - `/bin`, `/usr/bin` → essential binaries  

- Basic commands:
```bash
pwd        # show current directory
ls         # list files
cd /etc    # change directory
mkdir test # create folder
rmdir test # remove empty folder

🔹 File Permissions

Every file has owner, group, others with read (r), write (w), execute (x) permissions.

Example:

ls -l
-rwxr-xr--  1 mashu devops  123 Sep 9  script.sh


Change permissions:

chmod 755 script.sh
chmod +x script.sh
chown user:group file

🔹 Processes

Processes = running programs

Commands:

ps aux        # list processes
top           # show active processes
kill <PID>    # kill process by ID

🔹 Hands-On Practice (Docker Ubuntu)

Run Ubuntu container:

docker run -it ubuntu:latest /bin/bash


Inside container:

ls /
cd /home
mkdir devops-test
echo "Hello DevOps" > hello.txt
cat hello.txt
chmod +x hello.txt
ps aux


Exit container: exit

Start stopped container again:

docker ps -a
docker start -ai <container_name_or_id>
