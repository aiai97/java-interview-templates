# Linux Interview Questions and Answers

Short English answers for Java backend and Linux server interviews. Questions are grouped by practical interview frequency.

## 1. Linux Fundamentals — High Frequency

**Q1. What is Linux?**  
Linux is an open-source operating system kernel. Linux distributions combine the kernel with system tools, libraries, and applications.

**Q2. What is the difference between the kernel and the shell?**  
The kernel manages hardware and system resources. The shell interprets commands and provides a user interface to the operating system.

**Q3. What happens when you run a command in a shell?**  
The shell parses the command, locates the executable, creates a process, and waits for or tracks its result. The exact steps depend on whether the command is built in or external.

**Q4. What is a system call?**  
A system call is the interface a user-space program uses to request a service from the kernel, such as reading a file or creating a process.

**Q5. What is the difference between user mode and kernel mode?**  
User mode restricts direct access to hardware and protected memory. Kernel mode has the privileges needed to manage system resources.

**Q6. What is a Linux distribution?**  
A distribution packages the Linux kernel with utilities, libraries, a package manager, and other software, such as Ubuntu or Debian.

**Q7. What is the difference between an absolute path and a relative path?**  
An absolute path starts from the root directory `/`. A relative path is resolved from the current working directory.

**Q8. What do `grep`, `find`, and `xargs` do?**  
`grep` searches text, `find` locates filesystem entries, and `xargs` builds command arguments from input.

## 2. Processes and Signals — High Frequency

**Q9. What is a process?**  
A process is a running program with its own virtual address space and operating-system-managed resources.

**Q10. What is the difference between a process and a thread?**  
Processes normally have separate address spaces. Threads within a process share its address space and resources but have their own stacks and execution state.

**Q11. How do you inspect running processes?**  
Use `ps aux` for a process snapshot, `top` for live resource usage, and `pgrep` to find processes by name.

**Q12. What does `kill` do?**  
`kill` sends a signal to a process; it does not always terminate it immediately. For example, `kill -TERM PID` requests graceful termination.

**Q13. What is the difference between SIGTERM and SIGKILL?**  
SIGTERM asks a process to terminate and can be handled. SIGKILL forces termination and cannot be caught or ignored.

**Q14. What is a zombie process?**  
A zombie is a process that has exited but whose parent has not yet collected its exit status with a wait operation.

**Q15. What is an orphan process?**  
An orphan is a process whose parent has exited. It is typically reparented to a system process or subreaper.

**Q16. What does process state `D` mean?**  
`D` means uninterruptible sleep, commonly while waiting for certain kernel operations such as I/O. A process stuck in `D` may indicate an underlying resource or storage problem.

**Q17. What is a context switch?**  
A context switch is when the kernel stops one execution context and resumes another, saving and restoring the required state. Too many switches can add overhead.

**Q18. How do you check which process uses a port?**  
Use `ss -ltnp` for listening TCP sockets and associated process details when permitted. `lsof -i :PORT` is another option if installed.

## 3. Memory Management — High Frequency

**Q19. What is virtual memory?**  
Virtual memory gives each process its own virtual address space. The kernel and hardware translate virtual addresses to physical memory and enforce isolation.

**Q20. What is the difference between stack and heap memory?**  
The stack commonly stores function-call frames and local variables with automatic lifetime. The heap supports dynamically allocated memory whose lifetime is managed separately.

**Q21. What is a page fault?**  
A page fault occurs when memory access requires the operating system to resolve a page mapping or permission condition. It may be handled normally or may signal an invalid access.

**Q22. What is swap?**  
Swap provides disk-backed space for some memory pages. It can help under memory pressure, but heavy swapping can severely hurt performance.

**Q23. What is the Linux OOM killer?**  
When the system cannot satisfy memory demands, the kernel may terminate selected processes to recover memory.

**Q24. How do you investigate high memory usage?**  
Start with `free -h`, `top` or `ps`, then inspect `/proc/meminfo` and process-specific metrics. Distinguish process memory from filesystem cache and available memory.

**Q25. What is the difference between RSS and virtual memory size?**  
RSS is the amount of a process's memory currently resident in physical RAM. Virtual size includes mapped address space that may not be resident in RAM.

**Q26. Why can Linux show little “free” memory while still working normally?**  
Linux uses spare RAM for caches. The `available` value from `free -h` is often more useful than the raw `free` value for estimating memory available to applications.

## 4. Filesystems, File Descriptors, and Permissions — High Frequency

**Q27. What is an inode?**  
An inode stores file metadata and references to the file's data blocks. A filename is a directory entry that maps a name to an inode.

**Q28. What is a file descriptor?**  
A file descriptor is a small integer a process uses to refer to an open file, socket, pipe, or another I/O resource.

**Q29. What are standard input, standard output, and standard error?**  
They are file descriptors 0, 1, and 2, conventionally used for input, normal output, and error output.

**Q30. What does `chmod 755 file` mean?**  
The owner gets read, write, and execute permissions; the group and others get read and execute permissions.

**Q31. What is the difference between file permissions and ownership?**  
Ownership identifies the user and group associated with a file. Permission bits determine what the owner, group, and others may do.

**Q32. What does `umask` do?**  
`umask` removes permission bits from the permissions requested when new files or directories are created. It does not directly change existing files.

**Q33. What is a symbolic link?**  
A symbolic link is a filesystem entry that points to a path. It can refer to a file or directory and may become dangling if the target disappears.

**Q34. How do you find which files are using disk space?**  
Use `df -h` to check filesystem capacity and `du -sh PATH` to estimate usage under a directory. They answer different questions.

**Q35. Why can a disk be full even after a large file is deleted?**  
A process may still have the deleted file open. The space is released only after the final open reference is closed; `lsof +L1` can help find such files.

**Q36. What is the difference between `df` and `du`?**  
`df` reports filesystem-level space usage. `du` estimates space used by files and directories that it can traverse.

## 5. Networking — High Frequency for Backend Roles

**Q37. What is the difference between TCP and UDP?**  
TCP provides a reliable, ordered byte stream. UDP sends datagrams without guaranteeing delivery, ordering, or duplicate protection.

**Q38. What is a socket?**  
A socket is an operating-system interface for communication, commonly over a network or between local processes.

**Q39. What is the difference between a listening port and an established connection?**  
A listening socket waits for incoming connections. An established TCP connection represents an active connection between endpoints.

**Q40. How do you check network sockets on Linux?**  
Use `ss -lntp` for listening TCP sockets, `ss -ant` for TCP socket states, and `ip addr` to inspect network interfaces and addresses.

**Q41. What is DNS?**  
DNS maps domain names to records such as IP addresses. DNS failures can prevent a client from finding the server before a TCP connection begins.

**Q42. How would you debug a service that cannot be reached?**  
Check DNS resolution, the destination address and port, whether the service is listening, routing and firewall rules, and then test with tools such as `curl`, `nc`, and `tcpdump`.

**Q43. What is the difference between connection refused and connection timeout?**  
Connection refused usually means the destination actively rejected the connection, often because no service is listening. A timeout means no successful response arrived within the allowed time and may indicate packet filtering, routing, or an unresponsive endpoint.

**Q44. What does `TIME_WAIT` mean?**  
`TIME_WAIT` is a TCP state used after connection closure to help handle delayed packets and retransmissions safely. Many `TIME_WAIT` sockets are not automatically a problem.

**Q45. What is `epoll`?**  
`epoll` is a Linux API for monitoring readiness on many file descriptors. It is useful for scalable event-driven I/O servers.

## 6. Concurrency and Inter-Process Communication

**Q46. What is a pipe?**  
A pipe is a byte stream that lets processes pass data to one another, often through shell pipelines.

**Q47. What is shared memory?**  
Shared memory lets multiple processes access the same memory region. It can be fast, but concurrent access may require synchronization.

**Q48. What is a mutex?**  
A mutex provides mutual exclusion so only one thread at a time can enter a protected critical section.

**Q49. What is a semaphore?**  
A semaphore maintains a counter used to coordinate access to resources or signal events. Unlike a mutex, it is not necessarily tied to ownership by one thread.

**Q50. What is a race condition?**  
A race condition occurs when a result depends on the timing or interleaving of concurrent operations, often because shared state is not properly synchronized.

**Q51. What is a deadlock?**  
A deadlock occurs when tasks wait indefinitely for resources held by one another. Prevention techniques include consistent lock ordering and avoiding unnecessary nested locks.

## 7. Performance and Troubleshooting — Very Practical

**Q52. How do you investigate high CPU usage?**  
Use `top` or `pidstat` to identify the process and threads, then inspect logs and profile the workload. For deeper analysis, use `perf` or language-specific profiling tools.

**Q53. What is the difference between load average and CPU utilization?**  
CPU utilization measures how busy CPUs are over a period. Load average counts runnable tasks and tasks in uninterruptible sleep, so high load does not always mean high CPU utilization.

**Q54. How do you investigate high disk I/O latency?**  
Use `iostat -xz 1` to inspect device utilization and latency-related metrics, then identify the process and workload causing I/O with tools such as `iotop` or `pidstat` when available.

**Q55. What does `vmstat 1` show?**  
It reports memory, swap, process, CPU, and I/O-related statistics at one-second intervals. The first report may summarize activity since boot, so later reports are often more useful for current behavior.

**Q56. What is `strace` used for?**  
`strace` traces system calls and signals of a process. It can reveal slow or failing file, network, and process operations, though tracing adds overhead.

**Q57. What is `perf` used for?**  
`perf` is a Linux performance-analysis tool for profiling CPU usage, call stacks, and hardware or software events, depending on permissions and kernel support.

**Q58. How do you investigate a server that suddenly becomes slow?**  
Establish when the issue began, inspect CPU, memory, disk I/O, network, and process states, and correlate the results with logs and recent changes. Change one variable at a time when testing a suspected cause.

**Q59. What would you do if a server runs out of disk space?**  
Check `df -h`, find large directories with `du`, inspect logs and deleted-but-open files, and identify the growth source before cleaning up. Avoid deleting files blindly on a production system.

**Q60. How do you investigate a process that keeps restarting?**  
Check the service manager status and logs, inspect exit codes and signals, review resource limits and OOM events, and verify the application's own health checks and restart policy.

## 8. Linux Server and Production Scenarios

**Q61. What is `systemd`?**  
`systemd` is a system and service manager used by many Linux distributions to start services, manage dependencies, and collect logs.

**Q62. How do you inspect a service managed by systemd?**  
Use `systemctl status SERVICE` for status and `journalctl -u SERVICE` for its logs. Check the service unit and recent system events when it fails.

**Q63. What is the difference between `cron` and a systemd timer?**  
Both can schedule jobs. Cron uses cron schedules, while systemd timers integrate with service units and can provide systemd-specific dependency and logging behavior.

**Q64. What is a cgroup?**  
A control group organizes processes so the system can account for and limit resources such as CPU and memory. Containers commonly rely on cgroups for resource control.

**Q65. What is a container from the Linux perspective?**  
A container is a group of processes isolated using kernel features such as namespaces and constrained using mechanisms such as cgroups. It shares the host kernel rather than booting a separate kernel in the usual container model.

**Q66. What are namespaces?**  
Namespaces isolate views of system resources, such as process IDs, network interfaces, mount points, and hostnames. They are a core building block of Linux containers.

**Q67. What is the difference between a hard link and a symbolic link?**  
A hard link is another directory entry for the same inode and generally cannot cross filesystem boundaries. A symbolic link stores a path to its target and can cross filesystems.

**Q68. What is a file system mount?**  
Mounting attaches a filesystem to a directory in the unified directory tree, making its contents accessible at that mount point.

## 9. Advanced Topics

**Q69. What is the page cache?**  
The page cache keeps file data in RAM to reduce repeated storage reads. Linux can reclaim much of this cache when applications need memory.

**Q70. What is copy-on-write?**  
Copy-on-write lets processes or components share data until one needs to modify it. The system then creates a separate copy as needed, reducing unnecessary copying.

**Q71. What happens during `fork()`?**  
`fork()` creates a child process with a logical copy of the parent's process state. Memory is commonly managed with copy-on-write, so physical pages are not all copied immediately.

**Q72. What does `exec()` do?**  
An `exec` family call replaces the current process's program image with a new program. If it succeeds, it does not return to the old program code.

**Q73. What is the difference between `fork()` and `exec()`?**  
`fork()` creates a child process. `exec()` replaces a process's program image with another program.

**Q74. What is the difference between blocking and non-blocking I/O?**  
Blocking I/O may wait until an operation can proceed or complete. Non-blocking I/O returns promptly when it cannot proceed, allowing the program to perform other work.

**Q75. What is the difference between synchronous and asynchronous I/O?**  
Synchronous I/O makes the caller wait for the operation's completion or result. Asynchronous I/O lets the caller initiate work and receive completion later; exact semantics depend on the API.

## 10. Quick Command Reference

| Goal | Command | What to look for |
|---|---|---|
| CPU and processes | `top`, `ps aux` | CPU, memory, process state |
| Memory pressure | `free -h`, `vmstat 1` | Available memory, swap activity |
| Disk capacity | `df -h` | Filesystem space usage |
| Directory usage | `du -sh PATH` | Space used under a path |
| Disk I/O | `iostat -xz 1` | Device utilization and latency indicators |
| Network sockets | `ss -lntp` | Listening TCP ports and processes |
| Interface addresses | `ip addr` | IP addresses and interfaces |
| Service status | `systemctl status SERVICE` | Current service state and recent errors |
| Service logs | `journalctl -u SERVICE` | Service-related events |
| System calls | `strace -p PID` | System calls and failures |
| Open files | `lsof -p PID` | Files and sockets opened by a process |
| Deleted open files | `lsof +L1` | Open files whose directory entries were deleted |

## Interview Priority

Start with these topics if time is limited:

1. Process vs thread; SIGTERM vs SIGKILL; zombie process.
2. Virtual memory, RSS, swap, OOM, and Linux page cache.
3. Inode vs filename; file descriptor; `df` vs `du`; permissions.
4. TCP vs UDP; listening ports; DNS; connection refused vs timeout.
5. `top`, `free`, `vmstat`, `iostat`, `ss`, `journalctl`, and `strace`.
6. Real incidents: high CPU, memory pressure, full disk, and unreachable services.
