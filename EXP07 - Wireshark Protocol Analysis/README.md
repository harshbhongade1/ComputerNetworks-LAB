# Experiment 07: Analysis of Application Layer Protocols using Wireshark

**Name:** Kaustubh  
**PRN:** 24070521098  

---

## 1. Objective
To capture, filter, and inspect real-time application layer packets (DNS, HTTP) and transport layer packets (TCP, UDP) using the Wireshark Network Protocol Analyzer.

---

## 2. Tools Used
* **Wireshark Network Protocol Analyzer** (Windows / Ubuntu)
* **Target Interface:** Ethernet / Wi-Fi Network Adapter

---

## 3. Analysis of Captured Protocol Packets

### A. DNS Packet Analysis (Application Layer - Port 53)
* **Display Filter:** `dns`
* **Query Format:**
  * **Transaction ID:** A 16-bit identifier assigned by the client to match DNS queries with incoming responses.
  * **Flags:** Standard query (`0x0100`), Recursion Desired bit set (`RD = 1`).
  * **Questions Section:** Requested domain name (e.g., `google.com`), Query Type: `A` (Host address), Class: `IN` (Internet).
* **Response Format:**
  * **Flags:** Standard query response, No error (`rcode = 0`).
  * **Answers Section:** Returns the mapped IPv4/IPv6 addresses, Time to Live (TTL), and data length.

### B. TCP Three-Way Handshake Analysis (Transport Layer)
* **Display Filter:** `tcp.port == 80 || tcp.port == 443`
1. **SYN Packet:** Client sends SYN flag (`SYN = 1`, `Seq = 0`) to server to initiate connection.
2. **SYN-ACK Packet:** Server replies acknowledging the SYN (`ACK = 1`, `Ack = 1`) and sending its own SYN (`SYN = 1`, `Seq = 0`).
3. **ACK Packet:** Client confirms connection establishment (`ACK = 1`, `Seq = 1`, `Ack = 1`).
4. **Data Transfer & Connection Teardown:** Data frames exchanged followed by FIN/ACK sequence.

---

## 4. Key Wireshark Display Filters
* `dns` — Filters only DNS queries and responses.
* `dns.flags.response == 0` — Shows DNS queries only.
* `dns.flags.response == 1` — Shows DNS responses only.
* `ip.addr == 10.17.28.42` — Filters traffic to/from the local DNS server.
* `tcp.port == 80` — Filters HTTP traffic on port 80.
* `udp.port == 53` — Filters UDP datagrams carrying DNS payloads.
