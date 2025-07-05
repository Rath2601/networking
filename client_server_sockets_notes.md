# 📘 Computer Networking Notes

## 1. How Many Concurrent Sockets Can a Server Have?

A server can handle **thousands to millions** of concurrent sockets depending on:

| Factor | Description |
|--------|-------------|
| **OS File Descriptor Limit** | Sockets are treated as files. Default ~1024, can increase via `ulimit -n`. |
| **Memory Availability** | Each connection consumes memory for buffers and TCP state. |
| **Application Design** | Event-driven (e.g., Nginx, Node.js) handles more connections than thread-per-connection models. |
| **OS-Level Tuning** | Sysctl settings like `net.core.somaxconn`, `tcp_max_syn_backlog` impact limits. |
| **Port Exhaustion** | Server uses a fixed port, but clients use unique IP:port → no bottleneck on port reuse. |

> ✅ With proper tuning, modern servers can handle **100K to 1M+ concurrent connections**.

---

## 2. Difference Between Laptop/Desktop OS and Server OS

| Feature | Laptop/Desktop OS | Server OS |
|--------|--------------------|------------|
| **Purpose** | User-centric (UI, multimedia) | Backend tasks, services, hosting |
| **GUI** | GUI is default | Often headless (no GUI) |
| **Performance** | Less optimized for scale | Tuned for performance and stability |
| **Examples** | Windows 10/11, macOS, Ubuntu Desktop | Ubuntu Server, CentOS, Windows Server |
| **Uptime** | Can be turned off anytime | Designed for 24/7 uptime |
| **Security** | Focused on user protection | Hardened for production environments |
| **Peripherals** | Includes keyboard, monitor | Usually accessed remotely (SSH) |

> 🧠 Server OS is minimal, robust, and designed for **remote management** and **high availability**.

---

## 3. How Sockets Work in Client-Server Model

### 🔁 TCP Communication Steps

1. **Server Side:**
   - Creates socket and binds to known port (e.g., 80)
   - Calls `listen()` to wait for connections
   - Calls `accept()` to create a **new socket per client**

2. **Client Side:**
   - Creates socket using `socket()`
   - OS assigns **ephemeral port** (e.g., 49500)
   - Calls `connect()` to server's IP and port

3. **Connection Setup:**
   - TCP 3-way handshake (SYN → SYN-ACK → ACK)
   - On success, both ends have a connected socket

4. **Communication:**
   - Identified by this 4-tuple:
     ```
     <client IP, client port, server IP, server port>
     ```

5. **Closure:**
   - Either side can close
   - Socket enters `TIME_WAIT` state temporarily

> 📌 Server does **not receive** client’s socket — it **creates a new one** for each incoming connection.

---
