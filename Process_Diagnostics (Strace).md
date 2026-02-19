Вот аккуратно оформленный текст для вставки в `.md` файл, с сохранением структуры, команд и выделений. Я добавил **заголовки, блоки кода и списки**, чтобы было удобно читать на GitHub или в другом Markdown-рендерере:

````md
# Diagnosing Processes in Linux with strace

When a service hangs, is slow on startup, fails to open files, or behaves strangely, and the logs show nothing, the first tool to try is usually `strace`.  
It shows **system calls made by a process**, i.e., what the program is actually asking the kernel to do.

---

## Running a program under strace

```bash
strace ls /tmp
````

Immediately you can see:

* Which files are opened
* Which libraries are loaded
* Where errors occur

---

## Attaching to a running process

Useful if a service is already stuck:

```bash
sudo strace -p <PID>
```

Commonly, it becomes clear where it is blocked:

* `futex` — locks
* `poll` / `epoll_wait` — waiting for I/O
* `connect` — network attempts
* `read` / `write` — file or socket operations

---

## Tracing child processes

If the program spawns child processes, without `-f` some events won't appear:

```bash
strace -f <command>
```

---

## Tracing file operations

Check file access, open, stat, etc.:

```bash
strace -e trace=%file <command>
```

Example: finding missing files:

```bash
strace -e trace=%file <command> 2>&1 | grep ENOENT
```

You will see exactly which paths do not exist.

---

## Tracing network operations

```bash
strace -e trace=%network <command>
```

Shows:

* socket creation
* connection attempts
* errors

---

## Saving the output

```bash
strace -o trace.log <command>
```

For child processes:

```bash
strace -ff -o trace.log <command>
```

Separate files are created per PID.

---

## Adjusting output

* Increase string length (default is truncated):

```bash
strace -s 200 <command>
```

* Measure time spent in system calls:

```bash
strace -T <command>
```

* Short summary of system calls:

```bash
strace -c <command>
```

---

🔥 `strace` is invaluable for analyzing opaque binaries or when you do not have source code access.
It shows **where the process blocks** and **which operations actually occur in kernel space**.

---

🚪 [Linux Ready](https://t.me/+5rD10JtUCIwzN2Iy) | #practice

```

---

Если хочешь, я могу сделать **ещё более компактную cheat-sheet версию**, где команды и пояснения в виде таблицы — для **быстрого справочного использования в терминале**.  

Хочешь, чтобы я сделал такую версию?
```
