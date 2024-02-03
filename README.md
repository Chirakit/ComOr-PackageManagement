# Repository Set up & Package Management
- [Repository Set up \& Package Management](#repository-set-up--package-management)
  - [Package Management](#package-management)
    - [overview \& Concept](#overview--concept)
    - [Benefit](#benefit)
  - [apt](#apt)
  - [**YUM**](#yum)
    - [**How to install YUM in Ubuntu**](#how-to-install-yum-in-ubuntu)
    - [**Configuring Yum and Yum Repositories**](#configuring-yum-and-yum-repositories)
      - [**Setting \[main\] Options**](#setting-main-options)
      - [**Using Yum Variables**](#using-yum-variables)
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
ซึ่งช่วยให้สามารถตั้งค่า Yum ได้ และอีกส่วนคือ `[repository]` สามารถมีมากกว่า 1 repository ได้ ซึ่งช่วยให้สามารถตั้งค่าพื้นที่เก็บข้อมูลได้ อย่างไรก็ตาม แนะนำให้กำหนดพื้นที่เก็บแต่ละที่ในไฟล์ใหม่ หรือไฟล์ `.repo`
ที่อยู่ใน directory `/etc/yum.repos.d/` เราสามารถกำหนดค่าต่างๆ ในส่วน `[repository]`
ที่ไฟล์ `/etc/yum.conf` ได้ แล้วค่าต่างๆ ที่ทำการแก้ไขจะถูกอัพเดพเข้าไปที่ส่วนของ `[main]` ด้วย

ในส่วนนี้จะสอนการ :
- ตั้งค่า Yum โดยการแก้ไข configuration file ตรง `[main]` ที่ไฟล์ `/etc/yum.conf` 
- ตั้งค่า repositores ของแต่ละคนโดยแก้ไขที่ส่วนของ `[repository]` ใยไฟล์ `/etc/yum.conf` และไฟล์ `.repo` ซึ่งทั้ง 2 ไฟล์อยู่ใน directory `/etc/yum.repos.d/`
- ใช้ตัวแปร Yum ในไฟล์ `/etc/yum.conf` และไฟล์ที่อยู่ที่ directory `/etc/yum.repos.d/`     เพื่อให้เวอร์ชั่นมีความยืนหยุ่นและค่าของ architecture ได้รับการจัดการอย่างถูกต้อง
- เพิ่ม เปิดใช้งาน และปิดใช้งาน Yum repositories บน command line และตั้งค่า Yum repository ของตัวเองได้

#### **Setting [main] Options**
ไฟล์ configuration `/etc/yum.conf` ประกอบด้วยส่วนหลักเดียวคือ `[main]` และในขณะที่ value-key pairs บางส่วนส่งผลต่อการทำงานของ `yum` และการจัดการ repository เราสามารถเพิ่มตัวเลือกเพิ่มเติมในส่วนของข้อหัวของ `[main]` ในไฟล์ `/etc/yum.conf`

```
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=3

[comments แบบย่อ]

# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
```
ต่อไปนี้คือตัวเลือกที่ใช้บ่อยที่สุดในส่วน `[main]` :
\
\
**`assumeyes` =*value***
\
\
ค่าที่ใส่ *value* : \
`0` - `yum` ควรแสดงหน้าต่างยืนยันเมื่อมีการดำเนินการที่สำคัญ ค่านี้เป็นค่า default \
`1` - `yum` ไม่ต้องแสดงหน้าต่างยืนยันเมื่อมีการดำเนินการที่สำคัญ ถ้าค่า `assumeyes=1` `yum ` จะทำงานเหมือนกับการใช้ตัวเลือกคำสั่ง -y บน command line
\
\
**`cachedir` =*directory***
\
\
ค่า *directory* ต้องเป็น absolute path โดย Yum ควรจะเก็บข้อมูล cache และ database ในไฟล์ ถ้าไม่ได้กำหนดค่าอะไร (ค่า default) Yum's cache directory จะเก็บอยู่ที่ `/var/cache/yum/$basearch/$releasever`
\
\
สามารถดูข้อมูลได้ที่ [Using Yum Variables](#using-yum-variables) จะมีความหมายของตัวแปร `$basearch` และ `$releasever` อยู่
\
\
**`debuglevel` =*value***
\
\
ค่า *value* เป็นจำนวนเต็มระหว่าง `1` ถึง `10` การตั้งค่า `debuglevel` ให้มีค่าสูงขึ้นจะทำให้ yum แสดงผลลัพธ์ของการ debug ได้ละเอียดมากขึ้น `debuglevel=0` ปิดการแสดงผลของการ debug, ในขณะที่ `debuglevel=2` เป็นค่า default
\
\
**`exactarch` =*value***
\
\
ค่าที่ใส่ *value* : \
`0` - ไม่ต้องสนความถูกต้องสถาปัตยกรรมมากนัก เมื่อทำการอัปเดต package \
`1` - พิจารณาความถูกต้องของสถาปัตยกรรมเมื่อทำการอัปเดต package, yum จะไม่ติดตั้ง i686 package เพื่ออัปเดต i686 package ที่มีอยู่ในระบบแล้ว. หากไม่ได้กำหนดค่า `1` จะเป็นค่า default
\
\
**`exclude` =*package_name [more_package_names]***
\
\
ตัวเลือกนี้ช่วยให้สามารถยกเว้น package ที่ไม่อยากได้ตาม keyword ในระหว่างการติดตั้งหรืออัปเดต การระบุหลายๆ package ที่ไม่อยากได้สามารถทำได้โดยใส่ชื่อ package คั่นด้วยช่องว่าง และครอบด้วยเครื่องหมายคำพูด หรือได้ใช้ * หรือ ? ก็ได้
\
\
**`gpgcheck` =*value***
\
\
ค่าที่ใส่ *value* : \
`0` - ปิดใช้งาน GPG signature-checking บน package ทุกตัวใน repository ทั้งหมดที่มี รวมถึงการติดตั้ง package ที่มีอยู่ในเครื่อง \
`1` - เปิดใช้งาน GPG signature-checking บน package ทุกตัวใน repository ทั้งหมดที่มี รวมถึงการติดตั้ง package ที่มีอยู่ในเครื่อง `gpgcheck=1` เป็นค่า default ดังนั้น packages' signatures ทุกตัวจะถูกตรวจสอบ \
\
ถ้าตัวเลือกนี้ถูกตั้งค่าในส่วน `[main]` ของไฟล์ `/etc/yum.conf` จะกำหนดกฎ GPG-checking สำหรับ repository ทั้งหมดที่มี งั้นก็ตาม เราสามารถตั้งค่า `gpgcheck=value` สำหรับ repository แต่ละรายการได้ โดยการเปิดใช้งาน GPG-checking บน repository หนึ่งในขณะที่ปิดใช้งานบน repository อีกที่หนึ่ง การตั้งค่า gpgcheck=value สำหรับ repository แต่ละรายการในไฟล์ `.repo`  ที่เกี่ยวข้อง ค่า default จะถูกแทนที่ถ้ามีการระบุค่าใน ` /etc/yum.conf.` \
\
**`groupremove_leaf_only` =*value*** \
\
ค่าที่ใส่ *value* : \
`0` - yum จะไม่เช็ค dependencies ของแต่ละ package เมื่อกำลังจะลบ package group, yum จะลบทุก package ใน package group โดยไม่สนว่าจะมี package อะไรอยู่ข้างในหรือไหม `groupremove_leaf_only=0` เป็น default \
\
`1` - yum จะเช็คว่า dependencies ของแต่ละ package เมื่อกำลังจะลบ package group และลบเฉพาะ package ที่ไม่มีข้อมูลอะไรอยู่ข้างในเท่านั้น \
\
**`installonlypkgs` =*space separated list of packages*** \
\
เราสามารถแบ่งรายการ package ที่ `yum` สามารถติดตั้งได้ แต่จะไม่มีการอัปเดตเลย **yum.conf**(5) คือการดูรายการ package ที่เป็นแบบ install-only ตามค่า default \
\
หากเพิ่มคำสั่ง `installonlypkgs` ใน `/etc/yum.conf` เราควรแน่ใจว่ารายการทั้งหมดของ package ควรจะเป็นแบบ install-only รวมถึงรายการในส่วน `installonlypkgs` ของ **yum.conf**(5) ด้วย โดยเฉพาะ kernel packages ควรระบุใน `installonlypkgs` เสมอ (เหมือนกับค่า default) และ `installonly_limit` ควรถูกตั้งค่าเป็นค่าให้มีค่ามากกว่า `2` เพื่อให้มี kernel พร้อมใช้งานตลอดในกรณีที่ kernel ไม่สามารถ boot ได้เมื่อเกิดการ fail \
\
**`installonly_limit` =*value*** \
\
*value* เป็นจำนวนเต็มที่แทนจำนวนสูงสุดของเวอร์ชันที่สามารถติดตั้งพร้อมกันสำหรับ package แต่ละตัวที่ระบุในคำสั่ง installonlypkgs \
\
ค่า dafault สำหรับคำสั่ง installonlypkgs รวมถึง kernel packages ที่แตกต่างกันออกไป ดังนั้นควรระวังว่าการเปลี่ยนค่าของ installonly_limit จะส่งผลต่อจำนวนสูงสุดของเวอร์ชันที่ติดตั้งของ kernel package แต่ละตัว ค่า default ที่ระบุอยู่ใน /etc/yum.conf คือ installonly_limit=3 แล้วก็ไม่แนะนำให้ลดค่าๆ ให้ต่ำกว่า 2 ลงไป \
\
**`keepcache` =*value*** \
\
ค่าที่ใส่ *value* : \
`0` - จะไม่สำรอง cache ของ headers และหลังจากการติดตั้งเสร็จ `0` เป็นค่า default \
`1` - จะสำรอง cache หลังจากการติดตั้งเสร็จ \
\
**`logfile` =*file_name*** \
\
*file_name* ต้องเป็น absolute path ของไฟล์ที่ `yum` ควรเขียนผลลัพธ์การเข้าถึงบันทึกลงไป
โดยค่า default, `yum` จะเขียนบันทึกลงไปที่ `/var/log/yum.log`. \
\
**`multilib_policy` =*value*** \
\
ค่าที่ใส่ *value* : \
`best` - ติดตั้งสถาปัตยกรรมที่เหมาะสมที่สุดสำหรับระบบ เช่น ตั้งค่า `multilib_policy=best` บนระบบ AMD64 จะทำให้ `yum` ติดตั้งเวอร์ชัน 64-bit ของ package ทั้งหมด \
`all` — ติดตั้งทุกสถาปัตยกรรมที่เป็นไปได้สำหรับทุก package เช่น ถ้า `multilib_policy` ตั้งค่าเป็น `all` บนระบบ AMD64, `yum` จะติดตั้งทั้งเวอร์ชัน i686 และ AMD64 ของ package ถ้าสองระบบพร้อมใช้งาน \
\
**`obsoletes` =*value*** \
\
ค่าที่ใส่ *value* : \
`0` - ปิดใช้งานการประมวลผล logic ที่เก่าๆ ของ `yum` เมื่อทำการอัปเดต \
`1` - เปิดใช้งานการประมวลผล logic ที่เก่าๆ ของ `yum` เมื่อทำการอัปเดต เมื่อ package หนึ่งประกาศในไฟล์ spec ของมันว่ามีการตัดสิ่งที่เก่าทิ้ง แล้ว package นั่นจะถูกแทนที่ด้วย package ที่ไม่เอาเมื่อทำการติดตั้ง
obsoletes=1 เป็นค่า default \
\
**`plugins` =*value*** \
\
`0` - ปิดใช้งาน plug-in ของ yum ทั้งหมด \
`1` - เปิดใช้งาน plug-in ของ yum ทั้งหมด แต่ถ้าต้องการปิดใช้งาน plug-in ที่เฉพาะเจาะจงได้โดยการตั้งค่า `enabled=0` ใน configuration file ของ plug-in นั้น \
\
**`reposdir` =*directory*** \
\
*directory* เป็น absolute path ของ directory ที่ไฟล์ `.repo` ทั้งหมดถูกตั้งอยู่ ไฟล์ `.repo` ทุกไฟล์จะมีข้อมูล repository  (คล้ายกับในส่วนตรง `[repository]` ใน `/etc/yum.conf`)
`yum` รวบรวมข้อมูล repository ทั้งหมดจากไฟล์ `.repo` และส่วน `[repository]` ในไฟล์ `/etc/yum.conf` เพื่อสร้างรายการหลักของ repositories ที่จะใช้ในการทำ transaction ต่างๆ
ถ้า `reposdir` ไม่ได้ถูกตั้งค่า , `yum` จะใช้ default directory เป็น `/etc/yum.repos.d/` \
\
**`retries` =*value*** \
\
*value* เป็นจำนวนเต็ม `0` หรือมากกว่า ค่าๆ นี้คือจำนวนครั้งที่ `yum` ควรพยายามดึงไฟล์ก่อนที่จะคืนค่า error กลับมา การตั้งค่าเป็น `0` จะทำให้ `yum` ลองดึงไฟล์อีกครั้งและทำแบบนี้ต่อไปเรื่อยๆ ค่า default คือ `10`

#### **Using Yum Variables**

### Reference
- How To Install "yum" Package on Ubuntu \
  https://zoomadmin.com/HowToInstall/UbuntuPackage/yum
- Configuring Yum and Yum Repositories \
  https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-configuring_yum_and_yum_repositories


## Package Management Comparism
