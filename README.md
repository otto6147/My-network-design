

# Basic Multi-Subnet Network Design (Cisco Packet Tracer)

โปรเจกต์นี้เป็นการจำลองการออกแบบเครือข่ายพื้นฐานที่ประกอบด้วยหลายวงเครือข่าย (Multiple Subnets) โดยเน้นไปที่การทำงานร่วมกันของ **Router**, **Switch** และ **End Devices** เพื่อให้ข้อมูลสามารถรับ-ส่งข้ามวงแลนได้จริง

## โครงสร้างเครือข่าย (Network Architecture)

ในโปรเจกต์นี้เราจะแบ่งเครือข่ายออกเป็น 2 วง (LAN 1 และ LAN 2) โดยใช้ Router เป็นตัวกลางในการทำ **Inter-VLAN Routing** หรือ **Static Routing** พื้นฐาน:

* **Router:** ทำหน้าที่เป็น Gateway เชื่อมระหว่างเครือข่ายต่างวง
* **Switches:** ทำหน้าที่กระจายสัญญาณภายในวงแลนเดียวกัน
* **PCs/Laptops:** อุปกรณ์ปลายทางที่ใช้รับ-ส่งข้อมูล

## อุปกรณ์ที่ใช้ในโปรเจกต์

| อุปกรณ์ | รุ่นที่แนะนำ | จำนวน | หน้าที่ |
| --- | --- | --- | --- |
| **Router** | 2911 หรือ 4331 | 1 | เชื่อมต่อ Subnet ต่างๆ เข้าด้วยกัน |
| **Switch** | 2960 | 2 | เชื่อมต่ออุปกรณ์ภายใน LAN |
| **End Devices** | PC / Laptop | 4+ | อุปกรณ์ทดสอบการ Ping |

---

## รายละเอียดการตั้งค่า IP (IP Addressing Table)

| Interface | IP Address | Subnet Mask | Default Gateway |
| --- | --- | --- | --- |
| **Router G0/0 (LAN 1)** | 192.168.1.1 | 255.255.255.0 | - |
| **Router G0/1 (LAN 2)** | 192.168.2.1 | 255.255.255.0 | - |
| **PC0 (LAN 1)** | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| **PC1 (LAN 2)** | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |

---

## ขั้นตอนการตั้งค่า (Step-by-Step)

### 1. การตั้งค่าที่ Router

เพื่อให้ Router สามารถคุยกับอุปกรณ์ในแต่ละวงได้ เราต้องกำหนด IP ให้กับขา Interface:

```bash
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown

```

### 2. การตั้งค่าที่ PC

ไปที่เมนู **Desktop > IP Configuration** ของแต่ละเครื่อง:

* ระบุ **IP Address** ตามตารางด้านบน
* **สำคัญมาก:** ต้องระบุ **Default Gateway** ให้ตรงกับ IP ของขา Router ในวงนั้นๆ เพื่อให้ข้อมูลออกไปนอกวงได้

### 3. การทดสอบ (Testing)

เปิด Command Prompt ใน PC0 แล้วลองทดสอบส่งข้อมูลไปยัง PC1 ที่อยู่อีกวงหนึ่ง:

```bash
ping 192.168.2.10

```

> **หมายเหตุ:** การ Ping ครั้งแรกอาจจะขึ้น `Request timed out` เนื่องจากกระบวนการ ARP หลังจากนั้นจะขึ้น `Reply from...` แสดงว่าเชื่อมต่อสำเร็จ

---


# My-network-design
all network design I created 

## BasicTest 1: [file](https://github.com/otto6147/My-network-design/blob/main/BasicTest1.pkt)

<img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/a02b235f-68f0-47c6-890a-623160517a16" />


