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


## Day 5: Shell Scripting for Automation

### ✅ What I Learned
- Basics of creating and running shell scripts in Linux.
- Using `echo` to print messages.
- Automating cleanup tasks with `find`.
- Monitoring system resources (CPU, memory, disk).

### 📝 Hands-On Tasks
1. **greet.sh**  
   Prints a welcome message.  
   ```bash
   #!/bin/bash
   echo "Hello Mashu, welcome to DevOps Day 5!"
cleanup.sh
Deletes .tmp files older than 2 days from /tmp.

bash
Copy code
#!/bin/bash
find /tmp -name "*.tmp" -type f -mtime +2 -exec rm -f {} \;
echo "Cleanup complete."
monitor.sh
Displays CPU, memory, and disk usage.

bash
Copy code
#!/bin/bash
echo "===== System Monitoring ====="
echo "CPU Usage:"
top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4 "%"}'

echo ""
echo "Memory Usage:"
free -h | awk '/Mem:/ {print $3 " used / " $2 " total"}'

echo ""
echo "Disk Usage:"
df -h --total | grep 'total' | awk '{print $3 " used / " $2 " total (" $5 " used)"}'
echo "============================="
🚀 Outcome
Learned how to automate repetitive tasks using Bash.

Created simple scripts to greet, clean temporary files, and monitor system performance.

## Day 6–7: Mini Project (GitHub + Shell Scripts)

### ✅ What I Learned
- How to create and manage a GitHub repository for shell scripts.
- Basics of Git (clone, add, commit, push).
- Using shell scripts for simple automation:
  - Logging messages with timestamps.
  - Rotating logs to keep them manageable.
  - Creating project backups.

### 📝 Hands-On Tasks
1. **hello_log.sh**  
   Logs "Hello DevOps" with timestamp into a file.  
   ```bash
   #!/bin/bash
   LOG_DIR="./logs"
   LOG_FILE="$LOG_DIR/devops.log"

   mkdir -p $LOG_DIR
   echo "$(date '+%Y-%m-%d %H:%M:%S') - Hello DevOps" >> $LOG_FILE

   echo "Log entry added to $LOG_FILE"
rotate_logs.sh
Rotates devops.log if it is larger than 1KB, moving old logs into an archive folder.

bash
Copy code
#!/bin/bash
LOG_DIR="./logs"
LOG_FILE="$LOG_DIR/devops.log"
ARCHIVE_DIR="$LOG_DIR/archive"

mkdir -p $ARCHIVE_DIR

if [ -f "$LOG_FILE" ] && [ $(stat -c%s "$LOG_FILE") -gt 1024 ]; then
    TIMESTAMP=$(date '+%Y%m%d_%H%M%S')
    mv $LOG_FILE $ARCHIVE_DIR/devops_$TIMESTAMP.log
    echo "Log rotated. Archived as devops_$TIMESTAMP.log"
else
    echo "No rotation needed."
fi
backup.sh
Creates a .tar.gz backup of the project directory with a timestamp.

bash
Copy code
#!/bin/bash
SRC_DIR="."
BACKUP_DIR="./backups"
TIMESTAMP=$(date '+%Y%m%d_%H%M%S')
BACKUP_FILE="$BACKUP_DIR/devops_backup_$TIMESTAMP.tar.gz"

mkdir -p $BACKUP_DIR
tar -czf $BACKUP_FILE $SRC_DIR

echo "Backup created at $BACKUP_FILE"
🚀 Outcome
Learned to set up a GitHub repo for DevOps practice.

Automated logging, log rotation, and backups using Bash scripts.

Gained experience in structuring small projects with automation.

## Day 8: Continuous Integration & Continuous Delivery (CI/CD)

Today I learned the basics of **CI/CD** and created my first GitHub Actions pipeline.  

### 🔹 Key Learnings
- **CI (Continuous Integration):** Developers merge code frequently, and each change is automatically built & tested.  
- **CD (Continuous Delivery/Deployment):** Automates the process of deploying software after testing.  
- **Pipeline Stages:**  
  1. **Build** → Compile code & prepare artifacts  
  2. **Test** → Run unit & integration tests  
  3. **Deploy** → Deliver the build to staging/production  

### 🔹 Tools for CI/CD
- GitHub Actions (used today 🚀)  
- Jenkins, GitLab CI/CD, Azure Pipelines, TeamCity  

### 🔹 My First GitHub Actions Workflow
I created a `.github/workflows/ci.yml` file in my repo:

```yaml
name: DevOps Scripts CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Run sample script
      run: echo "🚀 Hello Mashu, your first CI pipeline is running!"
✅ Whenever I push to the main branch, this workflow runs automatically in the Actions tab.