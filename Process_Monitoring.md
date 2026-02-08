## Table of Contents

- [Process Monitoring (Linux)](#process-monitoring-linux)
- [Find a process by name](#find-a-process-by-name)
- [Basic process information](#basic-process-information-pid--23355)
- [Detailed process information](#detailed-process-information-procpid)
- [Near real-time view](#near-real-time-view)
- [Threads](#threads-count-and-details)
- [Open files and sockets](#open-files-and-sockets-file-descriptors)
- [Network connections](#network-connections-of-the-process)
- [Memory usage](#memory-usage)
- [CPU scheduling and priority](#cpu-scheduling-and-priority)
- [Executable and dependencies](#executable-and-dependencies)
- [Strace](#strace-runtime-behavior)
- [Troubleshooting a stuck process](#troubleshooting-a-stuck-process)

---

## Process Monitoring (Linux)

A quick reference for inspecting a running process using standard Linux tools and `/proc`.

---

### Find a process by name

Example: find processes with `CPP` in the name.

```bash
ps -ef | grep CPP
````

---

### Basic process information (PID = 23355)

```bash
ps -p 23355 -o pid,psr,ppid,user,stat,%cpu,%mem,etime,cmd
```

* `psr` — CPU core the process is currently running on

---

### Detailed process information (`/proc/<pid>`)

```bash
cat /proc/23355/status
```

Get the current CPU from `/proc/<pid>/stat`:

```bash
awk '{print $39}' /proc/23355/stat
```

---

### Near real-time view

Refresh process state and CPU usage every 200 ms:

```bash
watch -n 0.2 "ps -o pid,psr,%cpu,comm -p 23355"
```

---

### Threads (count and details)

List thread IDs:

```bash
ls /proc/23355/task
```

Detailed thread view:

```bash
ps -T -p 23355
```

---

### Open files and sockets (file descriptors)

```bash
ls -l /proc/23355/fd
lsof -p 23355
```

---

### Network connections of the process

```bash
ss -tp | grep 23355
lsof -Pan -p 23355 -i
```

---

### Memory usage

Memory mappings:

```bash
cat /proc/23355/maps
```

Detailed memory statistics:

```bash
cat /proc/23355/smaps
```

Quick summary:

```bash
grep -E 'VmRSS|VmSize|VmPeak' /proc/23355/status
```

---

### CPU scheduling and priority

```bash
ps -o pid,ni,pri,rtprio,policy,cmd -p 23355
cat /proc/23355/sched
```

---

### Executable and dependencies

Executable path:

```bash
readlink -f /proc/23355/exe
```

Current working directory:

```bash
readlink -f /proc/23355/cwd
```

Linked libraries:

```bash
ldd /proc/23355/exe
```

---

### Strace (runtime behavior)

Attach to a running process:

```bash
sudo strace -p 23355
```

Trace only file and network syscalls:

```bash
sudo strace -p 23355 -f -e trace=network,file
```

---

### Troubleshooting a stuck process

Check process state and wait channel:

```bash
ps -o pid,stat,wchan,cmd -p 23355
cat /proc/23355/wchan
```

Useful when diagnosing processes stuck in `D` (uninterruptible sleep) state.

```

---

Если хочешь, следующим шагом можем:
- привести **все файлы репы к единому стилю TOC**
- сделать ultra-compact **one-page cheat sheet**
- добавить разделы *CPU / Memory / I/O focused*
- или оформить это как **runbook для продакшена**

Говори, куда дальше двигаться.
```
