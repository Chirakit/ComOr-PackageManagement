# Repository Set up & Package Management
- [Repository Set up \& Package Management](#repository-set-up--package-management)
  - [Package Management](#package-management)
    - [overview \& Concept](#overview--concept)
    - [Benefit](#benefit)
  - [apt](#apt)
  - [**YUM**](#yum)
    - [**How to install YUM in Ubuntu**](#how-to-install-yum-in-ubuntu)
    - [**Configuring Yum and Yum Repositories**](#configuring-yum-and-yum-repositories)
    - [Reference](#reference)
  - [Package Management Comparism](#package-management-comparism)


## Package Management

### overview & Concept

### Benefit

## apt

## **YUM**

### **How to install YUM in Ubuntu**
1. เปิด command line terminal (ใช้ APT ในการติดตั้ง)
2. รันคำสั่ง ==update== เพื่ออัพเดต package repositories และรับข้อมูลจาก package ล่าสุด \
   `sudo apt-get update -y`
3. รันคำสั่งที่ติดตั้งด้วย ==-y== เพื่อความรวดเร็วในการติดตั้ง package \
   `sudo apt-get install -y yum`

### **Configuring Yum and Yum Repositories**
configuration file ของ `yum` จะเก็บอยู่ที่ `/etc/yum.conf` ไฟล์นี้ประกอบด้วยส่วนของ `[main]`
ซึ่งช่วยให้สามารถตั้งค่า Yum ได้ และอีกส่วนคือ `[repository]` สามารถมีมากกว่า 1 repository ได้ ซึ่ง
ช่วยให้สามารถตั้งค่าพื้นที่เก็บข้อมูลได้ อย่างไรก็ตาม แนะนำให้กำหนดพื้นที่เก็บแต่ละที่ในไฟล์ใหม่ หรือไฟล์ `.repo`
ที่อยู่ใน directory `/etc/yum.repos.d/` เราสามารถกำหนดค่าต่างๆ ในส่วน `[repository]`
ที่ไฟล์ `/etc/yum.conf` ได้ แล้วค่าต่างๆ ที่ทำการแก้ไขจะถูกอัพเดพเข้าไปที่ส่วนของ `[main]` ด้วย

ในส่วนนี้จะแสดงวิธีการ :
- ตั้งค่า Yum โดยการแก้ไข configuration file ตรง `[main]` ที่ไฟล์ `/etc/yum.conf` 
- 

### Reference
- How To Install "yum" Package on Ubuntu \
  https://zoomadmin.com/HowToInstall/UbuntuPackage/yum
- Configuring Yum and Yum Repositories \
  https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-configuring_yum_and_yum_repositories


## Package Management Comparism
