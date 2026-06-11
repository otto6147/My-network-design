# 🌐 My Network Design

> A collection of network design projects I built and tested in Cisco Packet Tracer — from basic multi-subnet routing to a full enterprise-grade design with firewall, wireless, and AAA.
>
> รวมโปรเจคออกแบบเครือข่ายที่ผมสร้างและทดสอบบน Cisco Packet Tracer ตั้งแต่ระดับพื้นฐานไปจนถึงระดับองค์กรครบวงจร

---

## 📑 Table of Contents / สารบัญ

1. [Basic Routing & Labs](#1-basic-routing--labs--พื้นฐาน) — พื้นฐาน routing, VLAN, multi-subnet
2. [TechStar Enterprise Network](#2-techstar-enterprise-network--โปรเจคใหญ่) — โปรเจคใหญ่ระดับองค์กร

---

# 1. Basic Routing & Labs / พื้นฐาน

โปรเจคพื้นฐานที่เน้นการทำงานร่วมกันของ **Router**, **Switch** และ **End Devices** เพื่อให้ข้อมูลรับ-ส่งข้ามวงแลนได้จริง ครอบคลุม Multi-Subnet Routing, VLAN และ Inter-VLAN Routing

### 🗂️ Lab Files / ไฟล์แต่ละ Lab

| Lab | Topic / หัวข้อ | File |
|---|---|---|
| **Basic Routing** | Multi-subnet routing พื้นฐาน | _(diagram below)_ |
| **BasicTest 1** | ทดสอบการเชื่อมต่อข้ามวง | [📄 BasicTest1.pkt](https://github.com/otto6147/My-network-design/blob/main/BasicTest1.pkt) |
| **LAB 2.1** | VLAN configuration | [📄 LAB2.1.pkt](https://github.com/otto6147/My-network-design/blob/main/6606475.LAB2.1.pkt) |
| **LAB 2.2** | VLAN + Trunking | [📄 LAB2.2.pkt](https://github.com/otto6147/My-network-design/blob/main/6606475%20Vlan%20LAB2.2.pkt) |
| **LAB 2.3** | Inter-VLAN Routing | [📄 LAB2.3](https://github.com/otto6147/My-network-design/blob/main/LAB2.3) |
| **LAB 4** | Advanced topology test | [📄 LAB4Test.pkt](https://github.com/otto6147/My-network-design/blob/main/LAB4Test.pkt) |

### 📸 Previews / ตัวอย่าง

**Basic Routing**

<img width="607" alt="Basic Routing" src="https://github.com/user-attachments/assets/89947005-e313-4209-bf67-3c06f283b9be" />

**BasicTest 1**

<img width="500" alt="BasicTest 1" src="https://github.com/user-attachments/assets/a02b235f-68f0-47c6-890a-623160517a16" />

**LAB 2.1**

<img width="700" alt="LAB 2.1" src="https://github.com/user-attachments/assets/37f00f56-5179-42a9-83ea-9c4573c9c97f" />

**LAB 2.2**

<img width="700" alt="LAB 2.2" src="https://github.com/user-attachments/assets/8c88738d-bacf-4a49-b8f5-44676a403fbf" />

**LAB 2.3**

<img width="474" alt="LAB 2.3" src="https://github.com/user-attachments/assets/c6e5b52c-0ee4-498f-9421-bfc93b91476d" />

**LAB 4 Test**

<img width="800" alt="LAB 4 Test" src="https://github.com/user-attachments/assets/15d21834-3d25-4229-bd39-f314623caa6e" />

<details>
<summary><b>📖 Basic Multi-Subnet Design — รายละเอียดการตั้งค่า (คลิกเพื่อดู)</b></summary>

<br>

แบ่งเครือข่ายออกเป็น 2 วง (LAN 1 และ LAN 2) โดยใช้ Router เป็น Gateway เชื่อมระหว่างวง

**Devices / อุปกรณ์ที่ใช้**

| อุปกรณ์ | รุ่นที่แนะนำ | จำนวน | หน้าที่ |
|---|---|---|---|
| **Router** | 2911 / 4331 | 1 | เชื่อม Subnet ต่างๆ เข้าด้วยกัน |
| **Switch** | 2960 | 2 | เชื่อมต่ออุปกรณ์ภายใน LAN |
| **End Devices** | PC / Laptop | 4+ | ทดสอบการ Ping |

**IP Addressing Table**

| Interface | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| Router G0/0 (LAN 1) | 192.168.1.1 | 255.255.255.0 | - |
| Router G0/1 (LAN 2) | 192.168.2.1 | 255.255.255.0 | - |
| PC0 (LAN 1) | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| PC1 (LAN 2) | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |

**Router Configuration**

\`\`\`bash
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
\`\`\`

**PC Setup** — ไปที่ \`Desktop > IP Configuration\` ของแต่ละเครื่อง ระบุ IP ตามตาราง และตั้ง **Default Gateway** ให้ตรงกับ IP ขา Router ในวงนั้น

**Testing** — เปิด Command Prompt ใน PC0 แล้ว ping ข้ามวง:

\`\`\`bash
ping 192.168.2.10
\`\`\`

> 💡 การ ping ครั้งแรกอาจขึ้น \`Request timed out\` เพราะกระบวนการ ARP หลังจากนั้นจะขึ้น \`Reply from...\` แสดงว่าเชื่อมต่อสำเร็จ

</details>

---

# 2. TechStar Enterprise Network / โปรเจคใหญ่

> Enterprise-grade, 4-floor company network designed and verified in Cisco Packet Tracer — Layer 2/3 switching, VLAN segmentation with policy-based access control, ASA firewall, centralized servers, and wireless.
>
> เครือข่ายองค์กรอาคาร 4 ชั้น ออกแบบและทดสอบบน Cisco Packet Tracer ครอบคลุม Switching, VLAN, การคุมสิทธิ์ข้ามแผนกด้วย ACL, ASA Firewall, Server Farm และ Wireless

### 🎯 Concept / แนวคิดของระบบ

ออกแบบเครือข่ายให้บริษัทที่มี 4 ชั้น แต่ละแผนกแยกเป็น VLAN ของตัวเอง โดยมี **Multilayer Switch (L3)** เป็นแกนกลางทำ Inter-VLAN Routing และใช้ **ACL คุมว่าแต่ละแผนกเข้าถึงแผนกไหนได้บ้าง** ตาม policy ขององค์กร ทางออกอินเทอร์เน็ตผ่าน **ASA Firewall** ที่ทำ NAT และเปิด web server สู่ภายนอกแบบ Static NAT

### 🏢 Building Layout / ผังอาคาร

| Floor / ชั้น | Departments / แผนก |
|---|---|
| **Floor 1** | Server Farm (DHCP, DNS, Web1, Web2, FTP, RADIUS), WLC, Multilayer Switch, IT |
| **Floor 2** | Accounting (บัญชี), HR |
| **Floor 3** | Sales, Marketing |
| **Floor 4** | (Access switch + Wireless coverage) |

### 🗺️ Topology / แผนผังเครือข่าย

![Topology](TechStar/topology/topology-diagram.png)

### 🔢 VLAN & Subnet Design / การออกแบบ VLAN และ Subnet

| Department / แผนก | VLAN | Subnet | Hosts |
|---|---|---|---|
| IT | 10 | 192.168.10.0/27 | ~20 |
| HR | 20 | 192.168.20.0/26 | ~40 |
| Sales | 30 | 192.168.30.0/26 | ~50 |
| Accounting (บัญชี) | 40 | 192.168.40.0/26 | ~40 |
| Marketing | 50 | 192.168.50.0/26 | ~50 |
| Meeting Room (ห้องประชุม) | 60 | 192.168.60.0/27 | ~15 |
| Server Room | 99 | 192.168.99.0/26 | servers |
| Executive (ผู้บริหาร) | 100 | 192.168.100.0/27 | — |

> 💡 ใช้ **VLSM** — แผนกใหญ่ (Sales/Marketing/HR) ได้ /26, แผนกเล็ก (IT/Meeting/CEO) ได้ /27 เพื่อใช้ IP อย่างคุ้มค่า

### 🔐 Access Control Policy / นโยบายการเข้าถึง (ACL)

หัวใจของดีไซน์ — ใช้ ACL บังคับว่าแต่ละแผนกคุยกับใครได้:

| Department | Access Rights / สิทธิ์การเข้าถึง |
|---|---|
| **IT** | ทุก VLAN (Admin) |
| **Executive (ผู้บริหาร)** | ทุก VLAN |
| **HR** | Server เท่านั้น |
| **Accounting** | Server เท่านั้น |
| **Sales** | Marketing + Server |
| **Marketing** | Sales + Server |
| **Meeting Room** | Internet เท่านั้น |

> รูปแบบ ACL: อนุญาตให้เข้า Server (VLAN 99) ก่อน → ปฏิเสธการเข้า internal subnet อื่น (192.168.0.0/16) → แล้วค่อย permit ออก internet (`permit any`) ซึ่งเป็นการทำ **least-privilege segmentation**

### 🛡️ Edge Security — ASA Firewall

| Feature | Implementation |
|---|---|
| **Security Zones** | inside (security 100) ↔ outside (security 0) |
| **Dynamic NAT/PAT** | ภายใน 192.168.0.0/16 → แปลงเป็น outside interface ออกเน็ต |
| **Static NAT** | Web1 (192.168.99.9 → 200.0.0.10), Web2 (192.168.99.7 → 200.0.0.11) เปิดสู่ภายนอก |
| **ACL (outside-in)** | อนุญาตเฉพาะ HTTP/HTTPS/ICMP เข้าหา web server |
| **Inspection** | ICMP inspection ผ่าน policy-map เพื่อให้ ping กลับได้แบบ stateful |

### 🖥️ Centralized Services / บริการรวมศูนย์

- **DHCP Server** (192.168.99.5) — แจก IP ให้ทุก VLAN ผ่าน `ip helper-address` บน L3 switch
- **DNS / Web1 / Web2 / FTP** servers ใน Server Farm (VLAN 99)
- **RADIUS Server** — สำหรับ AAA authentication ของ wireless

### 📶 Wireless

- **WLC (Wireless LAN Controller)** จัดการ **LWAP (Light Weight AP)** ทุกตัวทุกชั้นผ่าน CAPWAP
- Authentication ผ่าน RADIUS (WPA2-Enterprise)

### 🛠️ Skills Demonstrated / ทักษะที่แสดง

| Area | Implementation |
|---|---|
| **L3 Switching** | Inter-VLAN Routing via SVI, `ip routing` |
| **VLAN + VLSM** | 8+ VLAN, subnet ตามขนาดแผนกจริง |
| **Security (ACL)** | Policy-based segmentation, least privilege |
| **Firewall** | ASA — NAT/PAT, Static NAT, zone-based ACL, inspection |
| **Services** | DHCP relay (`ip helper-address`), DNS, Web, FTP |
| **Wireless** | WLC + LWAP + CAPWAP, RADIUS AAA |

### 💡 Key Technical Lessons / บทเรียนสำคัญ

- L3 switch ต้องเปิด `ip routing` ถึงจะทำ Inter-VLAN routing ได้
- ใช้ `ip helper-address` ชี้ไป DHCP server เพื่อให้ทุก VLAN ขอ IP จาก server กลางตัวเดียว
- ASA Static NAT จับคู่ private server กับ public IP เพื่อเปิดบริการสู่ภายนอกอย่างปลอดภัย
- ACL วางลำดับ permit/deny สำคัญมาก — permit สิ่งที่อนุญาตก่อน แล้วค่อย deny ที่เหลือ

### 📂 Project Structure / โครงสร้าง

```
TechStar/
├── README.md
├── topology/
│   └── topology-diagram.png      # 4-floor network topology
├── configs/                      # Device running-configs
│   ├── multilayer-switch-L3.txt  # Inter-VLAN routing + ACLs
│   ├── access-switches.txt       # L2 VLAN config
│   └── asa-firewall.txt          # NAT + firewall rules
└── docs/
    └── design-document.md        # VLAN/subnet/ACL design rationale
```
**Topologo diagram**


<img width="3555" height="2512" alt="present" src="https://github.com/user-attachments/assets/9acc6839-4f59-48ad-9004-ad6fcf957fe0" />
---


## 👤 Author

**Thanarak Kaewphaluek (Otto)** — Computer Engineering Student, Network Engineer track

📧 thanarak.k66@rsu.ac.th &nbsp;|&nbsp; 🔗 [github.com/otto6147](https://github.com/otto6147)
