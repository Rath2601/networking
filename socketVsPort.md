# 🔌 Socket vs Port – Summary Table

| Feature       | **Port**                                             | **Socket**                                                       |
|---------------|------------------------------------------------------|------------------------------------------------------------------|
| What is it?   | A 16-bit number (0–65535)                            | A full address that defines a single network connection          |
| Role          | Identifies a service on a machine                    | Uniquely identifies a session between two machines               |
| Components    | Just the number (e.g., 80, 443)                      | Source IP, Source Port, Destination IP, Destination Port, Protocol |
| Scope         | Local to a host                                      | Global (uniquely identifies connection)                          |
| Example       | `443` (HTTPS)                                        | `(192.168.0.5:54000 → 142.250.72.78:443)`                        |
| Unique?       | ❌ No (many apps can use same port at different IPs) | ✅ Yes (only one app can use the same socket)                    |
| Who uses it?  | OS and apps to listen for connections                | OS to manage individual sessions (e.g., TCP connection state)    |
| Protocol tie? | Used in both TCP & UDP                               | Always includes the protocol (TCP or UDP)                        |
