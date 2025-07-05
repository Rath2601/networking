# 🧠 Networking: Understanding Port Numbers

## 📌 What Is a Port?

- A **port** is a 16-bit software identifier (range: 0–65535).
- Used by the **Transport Layer (TCP/UDP)** to distinguish services on the same IP address.
- Think of ports as **virtual doors** for applications.

---

## ✅ Who Assigns Port Numbers?

- **IANA (Internet Assigned Numbers Authority)** maintains the official port number registry.
- Link: https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml

### 📊 Port Range Categories

| Range | Name | Description |
|-------|------|-------------|
| 0–1023 | **Well-known ports** | Reserved for core protocols (e.g., HTTP 80, SSH 22) |
| 1024–49151 | **Registered ports** | Used by 3rd-party applications (e.g., MySQL 3306) |
| 49152–65535 | **Dynamic/private ports** | Used for temporary outbound connections (ephemeral) |

---

## ⚙️ Where Are Ports Configured and Used?

- Ports are **not hardware-defined**.
- Managed by the **operating system**, specifically its **networking stack**.
- Applications **bind** to ports using system calls (`bind()`, `listen()`, etc.).
- Only **one app can bind to a port on a given IP** at a time.

---

## ❌ Do Port Numbers Exist in Hardware?

| Component | Knows About Ports? | How? |
|----------|---------------------|------|
| **NIC (Network Interface Card)** | ❌ No | Only deals with frames and raw data |
| **OS Kernel (TCP/IP Stack)** | ✅ Yes | Routes packets based on port numbers |
| **Applications** | ✅ Yes | Bind to specific ports to send/receive data |
| **Routers/Firewalls** | ✅ Partially | Inspect ports in packets for filtering/routing (software/firmware logic) |

---

## 🔍 Why Are There 65535 Ports?

- Port numbers use a **16-bit unsigned integer field**.
- 2¹⁶ = 65,536 → range: **0 to 65535**
- **Port 0** is reserved, often used for temporary/dynamic purposes.

---

## 🧠 Summary Table

| Question | Answer |
|---------|--------|
| Are ports physical? | ❌ No, they are software constructs |
| Who assigns ports? | ✅ IANA (standard port numbers) |
| Where are ports managed? | ✅ Inside OS (TCP/UDP stack) |
| Can apps change their port? | ✅ Yes, but clients must know the new port |
| Can hardware devices block ports? | ✅ Yes, using firewalls/ACLs, but they only **inspect**, not **store** them |

---

## 🛠️ Want to Try It?

- Use `netstat`, `ss`, or `lsof` to see which apps are using which ports.
- Use **Wireshark** to capture packets and view port numbers in headers.
