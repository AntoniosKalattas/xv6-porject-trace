# 🛠️ System Call Tracing in xv6
---

## 🔍 Objective

This extends the **xv6 operating system** by implementing a new system call: `trace`. This call allows **system call tracing** for the current process and its descendants.

---

## 🧪 What Was Implemented

A custom system call `trace(int mask)` was added. It enables system call tracing by setting a bitmask, where each bit corresponds to a specific system call. When a traced system call completes, the kernel prints:

- Process ID  
- System call name  
- Return value  

### ✅ Example Output

```bash
$ trace 32 grep hello README
3: syscall read -> 1023
3: syscall read -> 966
3: syscall read -> 70
3: syscall read -> 0
````

---

## 🛠️ Technical Summary

### 🔧 Kernel Modifications

* `sys_trace` added to `kernel/sysproc.c`
* Trace mask stored in `struct proc` (`kernel/proc.h`)
* System call numbers and names handled via `kernel/syscall.h` and a syscall name table
* Tracing logic added to `kernel/syscall.c`
* Fork inheritance: trace mask copied in `proc.c::fork()`
---

## ⚙️ How to Compile & Run

1. Clean and build xv6:

   ```bash
   make clean
   make qemu
   ```

2. Run with tracing:

   ```bash
   trace 2147483647 grep hello README
   ```

---
