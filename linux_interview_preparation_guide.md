# 🐧 Linux Scenario-Based Interview Questions & Answers

---

## 1. Disk Space Full

**Interviewer:** What would you do if a Linux server's disk space reaches 100%?

**Answer:**  
One scenario I prepared for is a server running out of disk space. First, I would check filesystem utilization using `df -h`. Then I would identify which directories are consuming the most space using `du -sh` and drill down into the relevant directories.

If large log files are responsible, I would identify old or unnecessary logs and follow the organization's log-retention process to clean them up. I would then verify the available space again using `df -h` and check whether the application has recovered.

Finally, I would investigate why the disk grew unexpectedly and consider log rotation, cleanup automation, or capacity expansion to prevent recurrence.

**Commands:**
```bash
df -h
du -sh /*
du -sh /var/log/*
find /var/log -type f -size +500M
```

---

## 2. Server Has High CPU Usage

**Interviewer:** A Linux server is showing 95–100% CPU. How would you troubleshoot?

**Answer:**  
First, I would confirm the CPU utilization using `top` or `htop`. Then I would identify which process is consuming the highest CPU. I would check whether the process is expected and whether there was a recent deployment or configuration change.

I would also check system load using `uptime` and review relevant logs. If required, I would escalate or restart the affected service according to the operational procedure rather than killing a production process without understanding the impact.

**Commands:**
```bash
top
htop
uptime
ps aux --sort=-%cpu | head
```

---

## 3. Server Running Out of Memory

**Interviewer:** How would you troubleshoot high memory utilization?

**Answer:**  
I would first check RAM and swap utilization using `free -h`. Then I would identify processes consuming the most memory using `top` or `ps`. I would check whether a particular application or process is continuously increasing its memory usage.

I would also check logs and recent changes. If the issue is caused by an application, I would coordinate with the application team rather than simply restarting the server.

**Commands:**
```bash
free -h
top
ps aux --sort=-%mem | head
```

---

## 4. Application Is Down

**Interviewer:** The application is not accessible. What would you check?

**Answer:**  
I would troubleshoot layer by layer. First, I would check whether the server is reachable. Then I would check whether the application service is running using `systemctl status`. After that, I would review service logs and check CPU, memory, and disk utilization.

If the service is stopped, I would follow the approved procedure to restart it and then verify that the application is accessible again.

**Commands:**
```bash
systemctl status nginx
systemctl status <service>
journalctl -u <service>
df -h
free -h
```

---

## 5. Permission Denied

**Interviewer:** You execute a shell script and receive *Permission denied*. What would you do?

**Answer:**  
First, I would check the file permissions using `ls -l`. If the execute permission is missing, I would use `chmod +x` according to the required access. I would then execute the script again and verify the result.

**Commands:**
```bash
ls -l script.sh
chmod +x script.sh
./script.sh
```

If ownership is also incorrect:
```bash
chown user:group script.sh
```

---

## 6. Nginx Is Not Working

**Interviewer:** Nginx is installed but the website is unavailable. What would you check?

**Answer:**  
I would first check the Nginx service status. If it is stopped, I would check the service logs and configuration. I would also verify whether the required port is listening and whether another process is using the port. After resolving the issue, I would restart or reload Nginx according to the situation and test the application again.

**Commands:**
```bash
systemctl status nginx
journalctl -u nginx
ss -lntp
nginx -t
systemctl restart nginx
```

---

## 7. Server Is Slow

**Interviewer:** Users report that a Linux server is very slow. How would you investigate?

**Answer:**  
I would start by checking CPU, memory, disk utilization, and system load. Then I would identify resource-intensive processes. I would also check whether the filesystem is full and review system/application logs for errors.

Based on the findings, I would determine whether the issue is CPU, memory, disk I/O, application-related, or another infrastructure issue.

**Commands:**
```bash
top
free -h
df -h
du -sh /*
uptime
journalctl -p err
```

---

## 8. SSH Login Is Failing

**Interviewer:** You cannot SSH into a Linux server. What would you check?

**Answer:**  
I would first verify network connectivity to the server. Then I would check whether the SSH service is running and whether port 22 is reachable. I would also verify the username, SSH key, permissions, and server-side authentication logs.

**Commands:**
```bash
ping <server-ip>
ssh user@<server-ip>
systemctl status ssh
ss -lntp | grep 22
```

For key-related issues:
```bash
ls -la ~/.ssh
```

---

## 9. Log Files Are Growing Rapidly

**Interviewer:** What would you do if `/var/log` suddenly became very large?

**Answer:**  
I would first identify which log files are consuming the space. Then I would determine whether the growth is expected or caused by an application error. I would not blindly delete active production logs. I would follow the organization's retention and log-rotation process, clean up only what is permitted, and investigate the underlying reason for the unusual log growth.

**Useful Commands:**
```bash
du -sh /var/log/*
ls -lh /var/log
```

---

## 10. A Process Is Not Responding

**Interviewer:** A Linux process is consuming resources and appears stuck. What would you do?

**Answer:**  
I would first identify the process and understand what service it belongs to. I would check its CPU and memory usage and review the relevant logs. If the process needs to be terminated, I would follow the approved operational procedure, starting with a graceful termination where appropriate rather than immediately using a force kill.

**Commands:**
```bash
ps aux
top
kill <PID>
```

---

## 🎯 A Strong Interview Pattern

For almost every Linux scenario, structure your answer like this:

1. **Identify** → What is the problem?
2. **Check** → Which command confirms it?
3. **Investigate** → What is causing it?
4. **Resolve** → What action would you take?
5. **Verify** → Did the issue actually get fixed?
6. **Prevent** → How can you stop it happening again?

### Workflow Example: Disk Full

```text
Identify filesystem (df -h)
        │
        ▼
Find large logs/files (du -sh)
        │
        ▼
Clean/rotate according to policy
        │
        ▼
Verify space restored (df -h)
        │
        ▼
Application verification
        │
        ▼
Root Cause + Preventive Action
```

> **Tip:** This **Identify → Investigate → Resolve → Verify → Prevent** approach will make your Linux interview answers sound much more structured than simply listing commands.