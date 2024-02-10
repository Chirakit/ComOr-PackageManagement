# Yellowdog Updater, Modified (YUM)
  - [**YUM คืออะไร**](#yum-คืออะไร)
  - [**Checking For and Updating Packages**](#checking-for-and-updating-packages)
  - [**How to install YUM in Ubuntu**](#how-to-install-yum-in-ubuntu)
  - [**Configuring Yum and Yum Repositories**](#configuring-yum-and-yum-repositories)
    - [**Setting \[main\] Options**](#setting-main-options)
    - [**Using Yum Variables**](#using-yum-variables)
    - [**Viewing the Current Configuration**](#viewing-the-current-configuration)
    - [**Adding, Enabling, and Disabling a Yum Repository**](#adding-enabling-and-disabling-a-yum-repository)
    - [**Adding a Yum Repository**](#adding-a-yum-repository)
    - [**Enabling a Yum Repository**](#enabling-a-yum-repository)
    - [**Disabling a Yum Repository**](#disabling-a-yum-repository)
    - [**Creating a Yum Repository**](#creating-a-yum-repository)
  - [**References**](#references)
<hr>

## YUM คืออะไร

YUM คือ โปรแกรมจัดการ package ที่ใช้กันในหลายระบบปฏิบัติการ Linux ที่มีความนิยมเช่น Fedora และ CentOS. YUM เป็นอินเตอร์เฟซ (front-end) สำหรับตัวจัดการ package จรูปแบบ RPM ซึ่งหมายความว่ามันจัดการกับ package ที่มีรูปแบบไฟล์ .rpm

เหมือนกับ APT, YUM ทำงานผ่านการใช้งานของฐานข้อมูลซอฟต์แวร์หรือที่เรียกว่า "repositories" หรือ "repos" ซึ่งเป็น Directories พิเศษที่เก็บรวมแพคเกจซอฟต์แวร์ต่าง ๆ Repositories มักจะถูกเก็บบนเซิร์ฟเวอร์ระยะไกลที่ผู้ใช้สามารถเข้าถึงผ่านการเชื่อมต่อเครือข่ายได้ แต่ก็เป็นไปได้ที่ผู้ใช้จะเก็บแพคเกจซอฟต์แวร์ในรีพอสิทอรีบนเครื่องที่ตั้งอยู่ภายในเครื่องของตนเองได้

"YUM" เป็นคำย่อที่มีความหมายว่า "Yellowdog Updater, Modified" ชื่อนี้นำกลับมาจากต้นกำเนิดของ YUM ที่เป็นการเขียนใหม่ของ Yellowdog UPdater (หรือที่รู้จักกันว่า "YUP") ซึ่งเป็นโปรแกรมอัปเดตซอฟต์แวร์สำหรับระบบปฏิบัติการ Yellow Dog Linux ที่ปัจจุบันไม่มีการพัฒนาต่อแล้ว. การเขียนใหม่ของ YUM เองนั้นได้ชื่อว่า Dandified YUM หรือ "DNF" ที่ได้ทำการแทนที่ YUM เป็นตัวจัดการ package เริ่มต้นใน Fedora และ Red Hat Enterprise Linux ในปัจจุบัน

## Checking For and Updating Packages

Yum ช่วยให้คุณตรวจสอบว่าระบบของคุณมีการอัปเดตใดที่รอการใช้งานอยู่หรือไม่. คุณสามารถแสดงรายการ package ที่ต้องการอัปเดตหรือจะอัปเดตทั้งหมดพร้อมกัน, หรือคุณสามารถอัปเดต package ที่ต้องการโดยเฉพาะได้

### Checking For Updates

เพื่อดูว่า package ที่ติดตั้งบนระบบของคุณมีการอัปเดตที่พร้อมใช้งานหรือไม่ ให้ใช้คำสั่งต่อไปนี้ :

```
~]# yum check-update
Loaded plugins: product-id, search-disabled-repos, subscription-manager
dracut.x86_64             033-360.el7_2   rhel-7-server-rpms
dracut-config-rescue.x86_64      033-360.el7_2   rhel-7-server-rpms
kernel.x86_64             3.10.0-327.el7   rhel-7-server-rpms
rpm.x86_64              4.11.3-17.el7   rhel-7-server-rpms
rpm-libs.x86_64            4.11.3-17.el7   rhel-7-server-rpms
rpm-python.x86_64           4.11.3-17.el7   rhel-7-server-rpms
yum.noarch              3.4.3-132.el7   rhel-7-server-rpms
```

package ที่แสดงในผลลัพธ์ด้านบนถูกรายชื่อว่ามีการอัปเดตที่พร้อมให้ใช้งาน. package แรกในรายการคือ dracut. ทุกบรรทัดในผลลัพธ์ตัวอย่างประกอบด้วยหลายแถว, ในกรณีของ dracut:
- `dracut` — ชื่อของ package
- `x86_64` — เวอร์ชันของ CPU ที่ package ถูกสร้างมาให้ใช้สำหรับ CPU เวอร์ชันนี้
- `033` — เวอร์ชันของ package ที่ถูกติดตั้ง
- `360.el7` — รุ่นหรือเวอร์ชันของ package ที่ได้รับการอัปเดต
- `_2` — รหัสเวอร์ชัน
- `rhel-7-server-rpms` — repository ที่เก็บ package ไว้


ผลลัพธ์แสดงว่าเราสามารถอัปเดต kernel (package kernel), yum และ RPM เอง (package yum และ rpm), รวมถึง package ที่ขึ้นอยู่กับพวกเขา (เช่น rpm-libs และ rpm-python) ทั้งหมดโดยใช้คำสั่ง yum.

### Updating Packages

คุณสามารถเลือกที่จะอัปเดต package เดี่ยว, หลาย package, หรือจะอัปเดตทั้งหมดพร้อมกัน. หากมีการอัปเดตที่ใช้งานอยู่สำหรับ package หรือ package ที่คุณกำลังอัปเดต และมี dependencies ที่มีการอัปเดตที่พร้อมใช้งาน, แล้ว dependencies นั้นๆ ก็จะถูกอัปเดตในคราวเดียวกันด้วย

Updating a Single Package

เพื่ออัปเดต package เดียว, ให้ใช้คำสั่งต่อไปนี้ในฐานะ `root` :

```
yum update package_name
```

**ตัวอย่าง :**

```
~]# yum update rpm
Loaded plugins: langpacks, product-id, subscription-manager
Updating Red Hat repositories.
INFO:rhsm-app.repolib:repos updated: 0
Setting up Update Process
Resolving Dependencies
--> Running transaction check
---> Package rpm.x86_64 0:4.11.1-3.el7 will be updated
--> Processing Dependency: rpm = 4.11.1-3.el7 for package: rpm-libs-4.11.1-3.el7.x86_64
--> Processing Dependency: rpm = 4.11.1-3.el7 for package: rpm-python-4.11.1-3.el7.x86_64
--> Processing Dependency: rpm = 4.11.1-3.el7 for package: rpm-build-4.11.1-3.el7.x86_64
---> Package rpm.x86_64 0:4.11.2-2.el7 will be an update
--> Running transaction check
...
--> Finished Dependency Resolution

Dependencies Resolved
=============================================================================
 Package          Arch    Version     Repository    Size
=============================================================================
Updating:
 rpm            x86_64   4.11.2-2.el7  rhel      1.1 M
Updating for dependencies:
 rpm-build         x86_64   4.11.2-2.el7  rhel      139 k
 rpm-build-libs      x86_64   4.11.2-2.el7  rhel       98 k
 rpm-libs         x86_64   4.11.2-2.el7  rhel      261 k
 rpm-python        x86_64   4.11.2-2.el7  rhel       74 k

Transaction Summary
=============================================================================
Upgrade 1 Package (+4 Dependent packages)

Total size: 1.7 M
Is this ok [y/d/N]:
```

เช่นเดียวกันกับการอัปเดต package แบบกลุ่ม ให้ใช้คำสั่งต่อไปนี้ในฐานะ `root`:

```
yum group update group_name
```

อัปเดต package ทั้งหมด

```
yum update
```

อัปเดต Security

```
yum update --security
```

หรือ

```
yum update-minimal --security
```

## Working with Packages

Yum ทำให้คุณสามารถดำเนินการกับ package ซอฟต์แวร์ได้ทั้งชุดครบถ้วน, รวมถึงการค้นหา package, ดูข้อมูลเกี่ยวกับ package, ติดตั้ง, และถอนการติดตั้ง

### Searching Packages

คุณสามารถค้นหาชื่อ package RPM, คำอธิบาย, และสรุปทั้งหมดได้โดยใช้คำสั่งต่อไปนี้:

```
yum search term&hellip;
```

เปลี่ยนจากคำว่า `term` เป็น package ที่คุณอยากค้นหา

**ตัวอย่าง :**

```
~]$ yum search vim gvim emacs
Loaded plugins: langpacks, product-id, search-disabled-repos, subscription-manager
============================= N/S matched: vim ==============================
vim-X11.x86_64 : The VIM version of the vi editor for the X Window System
vim-common.x86_64 : The common files needed by any version of the VIM editor
[output truncated]

============================ N/S matched: emacs =============================
emacs.x86_64 : GNU Emacs text editor
emacs-auctex.noarch : Enhanced TeX modes for Emacs
[output truncated]

 Name and summary matches mostly, use "search all" for everything.
Warning: No matches found for: gvim
```

## Listing Packages

เพื่อแสดงข้อมูลเกี่ยวกับ package ทั้งหมดที่ติดตั้งและที่มีให้ในปัจจุบัน, พิมพ์คำสั่งต่อไปนี้ที่หน้าต่าง shell:

```
yum list all
```


เพื่อแสดงรายการ package ที่ติดตั้งและที่มีให้ที่ตรงกับคำสั่ง glob expression ที่คุณใส่, ให้ใช้คำสั่งต่อไปนี้:

```
yum list glob_expression&hellip;
```

**ตัวอย่าง :**

```
~]$ yum list abrt-addon\* abrt-plugin\*
Loaded plugins: langpacks, product-id, search-disabled-repos, subscription-manager
Installed Packages
abrt-addon-ccpp.x86_64          2.1.11-35.el7       @rhel-7-server-rpms
abrt-addon-kerneloops.x86_64       2.1.11-35.el7       @rhel-7-server-rpms
abrt-addon-pstoreoops.x86_64       2.1.11-35.el7       @rhel-7-server-rpms
abrt-addon-python.x86_64         2.1.11-35.el7       @rhel-7-server-rpms
abrt-addon-vmcore.x86_64         2.1.11-35.el7       @rhel-7-server-rpms
abrt-addon-xorg.x86_64          2.1.11-35.el7       @rhel-7-server-rpms
```

เพื่อแสดงรายการ package ทั้งหมดที่ติดตั้งบนระบบของคุณ, ให้ใช้คำสั่งต่อไปนี้พร้อมกับคำสั่งคีย์ "installed" คำสั่งจะแสดงผลลัพธ์ทั้งหมดและคอลัมน์ทางขวาสุดในผลลัพธ์จะแสดงที่เก็บข้อมูลที่ package ถูกดึงมา.

```
yum list installed glob_expression&hellip;
```

**ตัวอย่าง :**

```
~]$ yum list installed "krb?-*"
Loaded plugins: langpacks, product-id, search-disabled-repos, subscription-manager
Installed Packages
krb5-libs.x86_64         1.13.2-10.el7          @rhel-7-server-rpms
```

เพื่อแสดงรายการ package ทั้งหมดที่มีในทุกที่เก็บข้อมูลที่เปิดใช้งานและพร้อมที่จะติดตั้ง, ให้ใช้คำสั่งต่อไปนี้ในรูปแบบต่อไปนี้:

```
yum list available glob_expression&hellip;
```

**ตัวอย่าง :**

```
~]$ yum list available gstreamer*plugin\*
Loaded plugins: langpacks, product-id, search-disabled-repos, subscription-manager
Available Packages
gstreamer-plugins-bad-free.i686       0.10.23-20.el7     rhel-7-server-rpms
gstreamer-plugins-base.i686         0.10.36-10.el7     rhel-7-server-rpms
gstreamer-plugins-good.i686         0.10.31-11.el7     rhel-7-server-rpms
gstreamer1-plugins-bad-free.i686      1.4.5-3.el7      rhel-7-server-rpms
gstreamer1-plugins-base.i686        1.4.5-2.el7      rhel-7-server-rpms
gstreamer1-plugins-base-devel.i686     1.4.5-2.el7      rhel-7-server-rpms
gstreamer1-plugins-base-devel.x86_64    1.4.5-2.el7      rhel-7-server-rpms
gstreamer1-plugins-good.i686        1.4.5-2.el7      rhel-7-server-rpms
```

**Listing Repositories**
เพื่อแสดงรายการ ID ของที่เก็บข้อมูล, ชื่อ, และจำนวน package สำหรับแต่ละที่เก็บข้อมูลที่เปิดใช้งานในระบบของคุณ, ให้ใช้คำสั่งต่อไปนี้:

```
yum repolist
```

เพื่อแสดงข้อมูลเพิ่มเติมเกี่ยวกับที่เก็บข้อมูลเหล่านี้, เพิ่มตัวเลือก `-v` เข้าไปในคำสั่ง. ด้วยตัวเลือกนี้เปิดใช้งาน, ข้อมูลรวมถึงชื่อไฟล์, ขนาดทั้งหมด, วันที่ของการอัปเดตล่าสุด, และ URL ของแหล่งเบสจะถูกแสดงสำหรับแต่ละที่เก็บข้อมูลที่รายการ. นอกจากนี้, คุณสามารถใช้คำสั่ง `repoinfo` ที่จะให้ผลลัพธ์เหมือนกัน

```
yum repolist -v
```
```
yum repoinfo
```

เพื่อแสดงรายการทั้งที่เปิดใช้งานและปิดใช้งาน, ให้ใช้คำสั่งต่อไปนี้. คอลัมน์ "สถานะ" ถูกเพิ่มเข้าไปในรายการผลลัพธ์เพื่อแสดงว่าที่เก็บข้อมูลไหนถูกเปิดใช้งาน

```
yum repolist all
```

โดยการส่ง `disabled` เป็น argument แรก, คุณสามารถลดผลลัพธ์คำสั่งเพื่อแสดงที่เก็บข้อมูลที่ถูกปิดใช้งานเท่านั้น. สำหรับการระบุเพิ่มเติม, คุณสามารถส่ง ID หรือชื่อของที่เก็บข้อมูลหรือ glob_expressions ที่เกี่ยวข้องเป็น argument . โปรดทราบว่าหากมีการตรงกันที่สมบูรณ์ระหว่าง ID หรือชื่อของที่เก็บข้อมูลกับ argument ที่ถูกใส่เข้าไป, ที่เก็บข้อมูลนี้จะถูกแสดงในรายการ แม้ว่าจะไม่ผ่านกรอง enabled หรือ disabled

## Displaying Package Information

เพื่อแสดงข้อมูลเกี่ยวกับหนึ่งหรือมากกว่าหนึ่ง package, ให้ใช้คำสั่งต่อไปนี้ (glob expressions สามารถใช้ได้ในที่นี้เช่นกัน):

```
yum info package_name&hellip;
```
เอาชื่อ package มาใส่ตรง package_name

**ตัวอย่าง :**

```
~]$ yum info abrt
Loaded plugins: langpacks, product-id, search-disabled-repos, subscription-manager
Installed Packages
Name    : abrt
Arch    : x86_64
Version   : 2.1.11
Release   : 35.el7
Size    : 2.3 M
Repo    : installed
From repo  : rhel-7-server-rpms
Summary   : Automatic bug detection and reporting tool
URL     : https://fedorahosted.org/abrt/
License   : GPLv2+
Description : abrt is a tool to help users to detect defects in applications and
      : to create a bug report with all information needed by maintainer to fix
      : it. It uses plugin system to extend its functionality.
```


คำสั่ง `yum info package_name` คล้ายกับคำสั่ง `rpm -q --info package_name`, แต่ให้ข้อมูลเพิ่มเติมที่ระบุชื่อของที่เก็บข้อมูล yum ที่แพคเกจ RPM ถูกติดตั้งมา (ดูที่บรรทัด `From repo:` ในผลลัพธ์).

**การใช้ yumdb**
คุณยังสามารถสอบถามฐานข้อมูล yum เพื่อดึงข้อมูลที่เป็นทางเลือกและมีประโยชน์เกี่ยวกับ package โดยใช้คำสั่งต่อไปนี้:

```
yumdb info package_name
```

คำสั่งนี้ให้ข้อมูลเพิ่มเติมเกี่ยวกับ package, รวมถึง check sum ของแพคเกจ (และขั้นตอนที่ใช้สร้าง, เช่น SHA-256), คำสั่งที่ใช้บนบรรทัดคำสั่งที่ถูกเรียกใช้เพื่อติดตั้ง package (ถ้ามี), และเหตุผลที่ package ถูกติดตั้งในระบบ (โดยที่ `user` ระบุว่าได้ถูกติดตั้งโดยผู้ใช้, และ `dep` หมายถึงมีการนำเข้ามาเนื่องจาก dependency)

**ตัวอย่าง :**
```
~]$ yumdb info yum
Loaded plugins: langpacks, product-id
yum-3.4.3-132.el7.noarch
   changed_by = 1000
   checksum_data = a9d0510e2ff0d04d04476c693c0313a11379053928efd29561f9a837b3d9eb02
   checksum_type = sha256
   command_line = upgrade
   from_repo = rhel-7-server-rpms
   from_repo_revision = 1449144806
   from_repo_timestamp = 1449144805
   installed_by = 4294967295
   origin_url = https://cdn.redhat.com/content/dist/rhel/server/7/7Server/x86_64/os/Packages/yum-3.4.3-132.el7.noarch.rpm
   reason = user
   releasever = 7Server
   var_uuid = 147a7d49-b60a-429f-8d8f-3edb6ce6f4a1
```

## Installing Packages
เพื่อติดตั้ง package เดี่ยวและทุก dependencies ที่ยังไม่ได้ติดตั้ง, ให้ใช้คำสั่งต่อไปนี้ในฐานะ `root`:
```
yum install package_name
```

คุณยังสามารถติดตั้งหลาย package พร้อมกันได้โดยการเพิ่มชื่อของ package เหล่านั้นเป็น arguments. เพื่อทำเช่นนั้น, พิมพ์ในฐานะ `root`:
```
yum install package_name package_name&hellip;
```

หากคุณกำลังติดตั้ง package ในระบบ multilib เช่นเครื่อง AMD64 หรือ Intel 64, คุณสามารถระบุโครงสร้างของแพคเกจ (ตราบเท่าที่มีในที่เก็บข้อมูลที่เปิดใช้งาน) โดยการเพิ่ม .arch ลงท้ายที่ชื่อ package :
```
yum install package_name.arch
```

**ตัวอย่าง :**
```
~]# yum install sqlite.i686
```

คุณสามารถใช้ glob expressions เพื่อติดตั้ง package หลายตัวที่มีชื่อคล้ายกันได้อย่างรวดเร็ว. ดำเนินการในฐานะ root ด้วยคำสั่งต่อไปนี้:
```
yum install glob_expression&hellip;
```

**ตัวอย่าง :**
```
~]# yum install audacious-plugins-\*
```

นอกจากชื่อ package และ glob expressions, คุณยังสามารถให้ชื่อไฟล์ให้กับ yum install ได้. หากคุณทราบชื่อของไบนารีที่คุณต้องการติดตั้ง แต่ไม่ทราบชื่อ package , คุณสามารถให้ yum install รับชื่อเส้นทางไฟล์. ทำเป็นผู้ดูแลระบบ (root):
```
yum install /usr/sbin/named
```

จากนั้น Yum จะค้นหาผ่านรายการ package ของมัน, พบ package ที่ `/usr/sbin/named`, หากมี, และจะขอคำยินยอมจากคุณว่าคุณต้องการติดตั้งหรือไม่
อย่างที่คุณเห็นในตัวอย่างข้างต้น, คำสั่ง yum install ไม่ต้องการ arguments ที่กำหนดไว้เป็นรูปแบบที่เข้มงวด. มันสามารถประมวลผลรูปแบบที่แตกต่างกันของชื่อ package และ glob expressions, ซึ่งทำให้การติดตั้งเป็นเรื่องที่สะดวกสบายสำหรับผู้ใช้. อย่างไรก็ตาม, มันจะใช้เวลาพักจนกว่า yum จะแปลงข้อมูลเข้าให้ถูกต้อง, โดยเฉพาะหากคุณระบุจำนวนมากของแพคเกจ. เพื่อเพิ่มประสิทธิภาพในการค้นหา package, คุณสามารถใช้คำสั่งต่อไปนี้เพื่อกำหนดโดยชัดเจนว่าต้องการแปลง arguments อย่างไร:

```
yum install-n name
```
```
yum install-na name.architecture
```
```
yum install-nevra name-epoch:version-release.architecture
```

**Installation Process**
```
~]# yum install httpd
Loaded plugins: langpacks, product-id, subscription-manager
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.4.6-12.el7 will be updated
---> Package httpd.x86_64 0:2.4.6-13.el7 will be an update
--> Processing Dependency: 2.4.6-13.el7 for package: httpd-2.4.6-13.el7.x86_64
--> Running transaction check
---> Package httpd-tools.x86_64 0:2.4.6-12.el7 will be updated
---> Package httpd-tools.x86_64 0:2.4.6-13.el7 will be an update
--> Finished Dependency Resolution

Dependencies Resolved
```
หลังจากที่ทำคำสั่งดังกล่าว yum จะโหลดปลั๊กอินที่จำเป็นและทำการตรวจสอบการทำธุรกรรม (transaction check) ในกรณีนี้ httpd ได้ถูกติดตั้งไว้แล้ว โดยที่เป็นเวอร์ชันเก่ากว่าเวอร์ชันล่าสุดที่มีอยู่ ดังนั้นจะทำการอัพเดท httpd เป็นเวอร์ชันล่าสุดที่มีอยู่ สถานะเดียวกันจะเป็นกับแพ็คเกจ httpd-tools ที่เป็นแพ็คเกจที่ httpd ขึ้นอยู่ จากนั้นจะแสดงสรุปของธุรกรรม (transaction summary)
```
================================================================================
 Package    Arch   Version         Repository        Size
================================================================================
Updating:
 httpd     x86_64  2.4.6-13.el7      rhel-x86_64-server-7  1.2 M
Updating for dependencies:
 httpd-tools  x86_64  2.4.6-13.el7      rhel-x86_64-server-7   77 k

Transaction Summary
================================================================================
Upgrade 1 Package (+1 Dependent package)

Total size: 1.2 M
Is this ok [y/d/N]:
```
ในขั้นตอนนี้ yum จะแสดงหน้าต่างยืนยันการติดตั้ง นอกจากตัวเลือก y (ใช่) และ N (ไม่) คุณยังสามารถเลือกตัวเลือก d (ดาวน์โหลดเท่านั้น) เพื่อดาวน์โหลดแพ็คเกจแต่ไม่ติดตั้งทันที หากคุณเลือก y, การติดตั้งจะดำเนินการต่อไปพร้อมกับข้อความต่อไปนี้จนกระทั่งเสร็จสิ้นโดยสำเร็จ
```
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
 Updating  : httpd-tools-2.4.6-13.el7.x86_64               1/4
 Updating  : httpd-2.4.6-13.el7.x86_64                  2/4
 Cleanup  : httpd-2.4.6-12.el7.x86_64                  3/4
 Cleanup  : httpd-tools-2.4.6-12.el7.x86_64               4/4
 Verifying : httpd-2.4.6-13.el7.x86_64                  1/4
 Verifying : httpd-tools-2.4.6-13.el7.x86_64               2/4
 Verifying : httpd-tools-2.4.6-12.el7.x86_64               3/4
 Verifying : httpd-2.4.6-12.el7.x86_64                  4/4

Updated:
 httpd.x86_64 0:2.4.6-13.el7

Dependency Updated:
 httpd-tools.x86_64 0:2.4.6-13.el7

Complete!
```
## Downloading Packages
ตามที่แสดงในตัวอย่าง "Installation Process", ในขั้นตอนการติดตั้งที่บางจุดคุณจะได้รับคำถามเพื่อยืนยันการติดตั้งด้วยข้อความต่อไปนี้:
```
...
Total size: 1.2 M
Is this ok [y/d/N]:
...
```
ด้วยตัวเลือก d, yum จะดาวน์โหลดแพ็คเกจโดยไม่ติดตั้งทันที คุณสามารถติดตั้งแพ็คเกจเหล่านี้ภายหลังได้โดยใช้คำสั่ง yum localinstall หรือคุณยังสามารถแบ่งปันแพ็คเกจกับอุปกรณ์อื่น ๆ ได้ แพ็คเกจที่ดาวน์โหลดจะถูกบันทึกไว้ในหนึ่งในไดเรกทอรีย่อยของไดเรกทอรีแคช โดยค่าเริ่มต้นคือ /var/cache/yum/$basearch/$releasever/packages/ การดาวน์โหลดจะดำเนินการในโหมดพื้นหลังเพื่อให้คุณสามารถใช้ yum สำหรับการดำเนินการอื่น ๆ ได้พร้อมกัน

## Removing Packages
เหมือนกับการติดตั้งแพ็คเกจ, yum ยังช่วยให้คุณถอนการติดตั้งแพ็คเกจได้ด้วยคำสั่ง uninstall. เพื่อถอนการติดตั้งแพ็คเกจที่ระบุ, รวมถึงแพ็คเกจทั้งหมดที่ขึ้นอยู่กับมัน, ให้ทำการรันคำสั่งต่อไปนี้ในฐานะ root:
```
yum remove package_name&hellip;
```
เช่นเดียวกับคำสั่ง `install`, คำสั่ง `remove` ก็สามารถใช้ arguments เหล่านี้ได้:
- package names
- glob expressions
- file lists
- package provides

<hr>

## **How to install YUM in Ubuntu**
1. เปิด command line terminal (ใช้ APT ในการติดตั้ง)
2. รันคำสั่ง `update` เพื่ออัพเดต package repositories และรับข้อมูลจาก package ล่าสุด \
   `sudo apt-get update -y`
3. รันคำสั่งที่ติดตั้งด้วย `-y` เพื่อความรวดเร็วในการติดตั้ง package \
   `sudo apt-get install -y yum`

## **Configuring Yum and Yum Repositories**
configuration file ของ `yum` จะเก็บอยู่ที่ `/etc/yum.conf` ไฟล์นี้ประกอบด้วยส่วนของ `[main]`
ซึ่งช่วยให้สามารถตั้งค่า Yum ได้ และอีกส่วนคือ `[repository]` สามารถมีมากกว่า 1 repository ได้ ซึ่งช่วยให้สามารถตั้งค่าพื้นที่เก็บข้อมูลได้ อย่างไรก็ตาม แนะนำให้กำหนดพื้นที่เก็บแต่ละที่ในไฟล์ใหม่ หรือไฟล์ `.repo`
ที่อยู่ใน directory `/etc/yum.repos.d/` เราสามารถกำหนดค่าต่างๆ ในส่วน `[repository]`
ที่ไฟล์ `/etc/yum.conf` ได้ แล้วค่าต่างๆ ที่ทำการแก้ไขจะถูกอัพเดพเข้าไปที่ส่วนของ `[main]` ด้วย

ในส่วนนี้จะสอนการ :
- ตั้งค่า Yum โดยการแก้ไข configuration file ตรง `[main]` ที่ไฟล์ `/etc/yum.conf` 
- ตั้งค่า repositores ของแต่ละคนโดยแก้ไขที่ส่วนของ `[repository]` ใยไฟล์ `/etc/yum.conf` และไฟล์ `.repo` ซึ่งทั้ง 2 ไฟล์อยู่ใน directory `/etc/yum.repos.d/`
- ใช้ตัวแปร Yum ในไฟล์ `/etc/yum.conf` และไฟล์ที่อยู่ที่ directory `/etc/yum.repos.d/`     เพื่อให้เวอร์ชั่นมีความยืนหยุ่นและค่าของ architecture ได้รับการจัดการอย่างถูกต้อง
- เพิ่ม เปิดใช้งาน และปิดใช้งาน Yum repositories บน command line และตั้งค่า Yum repository ของตัวเองได้

### **Setting [main] Options**
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
ถ้า `reposdir` ไม่ได้ถูกตั้งค่า , `yum` จะใช้ default directory เป็น `/etc/yum.repos.d/`
\
**`retries` =*value*** \
\
*value* เป็นจำนวนเต็ม `0` หรือมากกว่า ค่าๆ นี้คือจำนวนครั้งที่ `yum` ควรพยายามดึงไฟล์ก่อนที่จะคืนค่า error กลับมา การตั้งค่าเป็น `0` จะทำให้ `yum` ลองดึงไฟล์อีกครั้งและทำแบบนี้ต่อไปเรื่อยๆ ค่า default คือ `10` \

### Setting [repository] Options
ส่วน `[repository]` repository จะมี Unique ID เป็นของตัวเอง ช่วยให้กำหนด Yum repositories ของแต่ละตัวได้ง่าย เพื่อป้องกันการซ้ำ
ของ ID \

ยกตัวอย่างสิ่งที่ต้องมีขั้นต่ำในส่วนของ `[repository]`
```
[repository]
name=repository_name
baseurl=repository_url
```
ในส่วนของ `[repository]` หลักๆ ที่ต้องจำเป็นต้องมีคือ : \
\
**`name`=*repository_name*** \
\
*repository_name* คือชื่อของ repository ที่เราตั้งขึ้น \
\
**`baseurl`=*repository_url*** \
\
*repository_url* เป็น url ที่ link ไปที่ directory ที่ `datarepo` ของ repository ถูกตั้งอยู่ :
- หาก repository นั้นให้บริการผ่าน HTTP ให้ใช้ `http://path/to/repo`
- หาก repository นั้นให้บริการผ่าน FTP ให้ใช้ `ftp://path/to/repo`
- หาก repository อยู่เคริ่องของเรา ให้ใช้: `file:///path/to/local/repo`

แต่โดยโดยปกติ URL ส่วยใหญ่จะเป็น HTTP link, เช่น : \
`baseurl=http://path/to/repo/releases/$releasever/server/$basearch/os/`

แล้วก็จะมีคำสั่งที่มีค่อนข้างประโยชน์ในส่วน `[repository]` ด้วย : \
\
**`enable`=*value*** \
\
ค่าที่ใส่ value : \
`0` - ไม่รวม repository นี้เป็น package source เมื่อทำการอัปเดตและติดตั้ง ซึ่งเป็นวิธีที่ง่ายที่สุดที่ใช้เปิด-ปิด repository แบบเร็วๆ
มันจะมีประโยชน์ตรงที่ต้องการ package อย่างเดียวจาก repository \
`1` - รวม repository นี้เป็น package source 

การเปิดและปิด repository ยังสามารถทำได้โดยการส่งค่า `--enablerepo=repo_name` หรือ `--disablerepo=repo_name` ให้กับ yum 
หรือใช้หน้าต่าง **Add/Remove Software** ของโปรแกรม **PackageKit** ก็ได้

ต่อไปนี้คือตัวอย่างไฟล์ `/etc/yum.repos.d/redhat.repo` :
```
#
# Red Hat Repositories
# Managed by (rhsm) subscription-manager
#

[red-hat-enterprise-linux-scalable-file-system-for-rhel-6-entitlement-rpms]
name = Red Hat Enterprise Linux Scalable File System (for RHEL 6 Entitlement) (RPMs)
baseurl = https://cdn.redhat.com/content/dist/rhel/entitlement-6/releases/$releasever/$basearch/scalablefilesystem/os
enabled = 1
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
sslverify = 1
sslcacert = /etc/rhsm/ca/redhat-uep.pem
sslclientkey = /etc/pki/entitlement/key.pem
sslclientcert = /etc/pki/entitlement/11300387955690106.pem

[red-hat-enterprise-linux-scalable-file-system-for-rhel-6-entitlement-source-rpms]
name = Red Hat Enterprise Linux Scalable File System (for RHEL 6 Entitlement) (Source RPMs)
baseurl = https://cdn.redhat.com/content/dist/rhel/entitlement-6/releases/$releasever/$basearch/scalablefilesystem/source/SRPMS
enabled = 0
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
sslverify = 1
sslcacert = /etc/rhsm/ca/redhat-uep.pem
sslclientkey = /etc/pki/entitlement/key.pem
sslclientcert = /etc/pki/entitlement/11300387955690106.pem

[red-hat-enterprise-linux-scalable-file-system-for-rhel-6-entitlement-debug-rpms]
name = Red Hat Enterprise Linux Scalable File System (for RHEL 6 Entitlement) (Debug RPMs)
baseurl = https://cdn.redhat.com/content/dist/rhel/entitlement-6/releases/$releasever/$basearch/scalablefilesystem/debug
enabled = 0
gpgcheck = 1
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
sslverify = 1
sslcacert = /etc/rhsm/ca/redhat-uep.pem
sslclientkey = /etc/pki/entitlement/key.pem
sslclientcert = /etc/pki/entitlement/11300387955690106.pem
```

### **Using Yum Variables**
`$releasever` \
ตัวแปรนี้เพื่ออ้างอิงเวอร์ชั่น โดย Yum ได้รับค่าของ `$releasever` จากบรรทัด `distroverpkg=value` ในไฟล์
/etc/yum.conf เช่น 6Client, 6Server

`$arch` \
ตัวแปรนี้เพื่ออ้างถึงสถาปัตยกรรม CPU ของระบบตามผลลัพธ์ที่ได้จากการเรียกใช้ฟังก์ชั่น os.uname() ใน Python

`$basearch` \
ใช้ $basearch เพื่ออ้างถึงสถาปัตยกรรมหลักของระบบคอมพิวเตอร์ เช่น x86_64, AMD64

`$YUM0-9` \
ทั้ง 10 ตัวแปร (YUM0, YUM1, ..., YUM9) ถูกแทนที่ด้วย environment variables ของ shell ที่มีชื่อเดียวกัน หากอ้างถึงหนึ่งในตัวแปร
(ใน /etc/yum.conf เป็นตัวอย่าง) และ environment variable ของ shell ที่ไม่ใช่ชื่อเดียวกัน แล้วตัวแปรของ configuration ค่าจะไม่ถูกแทนที่

เพื่อกำหนดตัวแปรเองหรือที่ต้องการแทนค่าของตัวแปรที่มีอยู่ สร้างไฟล์ที่มีชื่อเดียวกับตัวแปร (โดยไม่ต้องมีเครื่องหมาย “$”) ใน directory `/etc/yum/vars`
และเพิ่มค่าที่ต้องการลงบนบรรทัดแรกของไฟล์

ยกตัวอย่างเช่น \
คำอธิบายของ repository รวมถึงชื่อ OS เพื่อนิยามตัวแปรใหม่ที่เรียกว่า `$osname` สร้างไฟล์ใหม่พร้อม “Red Hat Enterprise Linux”
บนบรรทัดแรก และบันทึกไฟล์ที่ `/etc/yum/vars/osname` : 

`~]# echo "Red Hat Enterprise Linux" > /etc/yum/vars/osname`

ถ้าแทนที่ด้วย 'Red Hat Enterprise Linux 6' สามารถแก้ไขไฟล์ได้ในไฟล์ `.repo` :
`name=$osname $releasever`

### Viewing the Current Configuration
เพื่อแสดงค่าปัจจุบันของ Yum options ทั้งหมด (มันก็คือตัวเลือกที่ระบุในส่วน `[main]` ของไฟล์ `/etc/yum.conf`), ให้ run `yum-config-manager`
โดยไม่ใส่ตัวเลือกบน command-line : 

`yum-config-manager`

เพื่อแสดงรายการเนื้อหาในของส่วนการกำหนดค่าที่แตกต่างกันแค่ส่วนเดียวหรือตรงส่วนอื่นๆ ให้ใช้คำสั่งนี้:

`yum-config-manager section`

แล้วยังสามารถใช้ glob expression เพื่อแสดงการกำหนดค่าของทุกส่วนที่ตรงกัน :

`yum-config-manager glob_expression`

ยกตัวอย่างเช่น ถ้าอยากให้แสดงรายการทุกตัวเลือกการกำหนดค่า และแสดงค่าที่สอดคล้องกัน ให้พิมพ์คำสั่งนี้ลงใน shell prompt :
```
~]$ yum-config-manager main \*
Loaded plugins: product-id, refresh-packagekit, subscription-manager
================================== main ===================================
[main]
alwaysprompt = True
assumeyes = False
bandwith = 0
bugtracker_url = https://bugzilla.redhat.com/enter_bug.cgi?product=Red%20Hat%20Enterprise%20Linux%206&component=yum
cache = 0
[output truncated]
```

### **Adding, Enabling, and Disabling a Yum Repository**
ในข้อหัว [Setting [repository] Options](#setting-repository-options) ได้บอกถึงตัวเลือกต่าง ๆ ที่สามารถใช้เพื่อกำหนด 
Yum repository ได้ ในหัวข้อนี้จะอธิบายวิธีการเพิ่ม เปิดใช้งาน และปิดใช้งาน repository โดยใช้คำสั่ง `yum-config-manager`

#### Adding a Yum Repository
การเพิ่ม repository นั้น สามารถเพิ่มตรงส่วน `[repository]` ในไฟล์ `/etc/yum.conf` หรือไฟล์ `.repo` ที่อยู่ตรง directory
`/etc/yum.repos.d/` ไฟล์ทั้งหมดที่มีนามสกุล .repo ต่อท้าย directory นี้จะถูกอ่านโดย yum

Yum repositories แต่ละอันจะมีไฟล์ `.repo` ของแต่ตัวเอง เพื่อทำการเพิ่ม repository เช่น เราต้องการติดตั้งระบบต่างแล้วเปิดใช้งาน
ให้รันคำสั่งนี้ (username เราต้องเป็น root) :
1. `sudo su` -> เข้าถึง root (ถ้ามี password ให้ใส่ password ด้วย มันจะเป็น password เดียวกับตอนที่ login เข้าใช้งาน ubuntu)
2. `yum-config-manager --add-repo repository_url` -> ใส่คำสั่งนี้เข้าไป

ตรง *repository_url* เป็น link ที่พาไปที่ไฟล์ `.repo` เช่น ใส่ link http://www.example.com/example.repo เพื่อเพิ่มที่ตั้งของ repository
เราสามารถใส่คำสั่งนี้ลงไปใน shell prompt ได้ :
```
~]# yum-config-manager --add-repo http://www.example.com/example.repo
Loaded plugins: product-id, refresh-packagekit, subscription-manager
adding repo from: http://www.example.com/example.repo
grabbing file http://www.example.com/example.repo to /etc/yum.repos.d/example.repo
example.repo                                             |  413 B     00:00
repo saved to /etc/yum.repos.d/example.repo
```

#### Enabling a Yum Repository
การเปิดใช้งาน repository ที่เฉพาะเจาะจงนั้น เราต้องใช้ยศ root แล้วพิมพ์คำสั่งนี้ลงใน shell prompt :

`yum-config-manager --enable repository`

ืตัวแปร *repository* ตรงคำสั่งเมิ่อกี้ จะเป็น unique ID ของ repository (ใช้คำสั่ง `yum repolist all` เพื่อลิสต์รหัส repository 
ทั้งหมดที่มี) อีกวิธีคือใช้ glob expression เพื่อเปิดใช้งาน repository ทั้งหมดที่ตรงกัน :

`yum-config-manager --enable glob_expression`

ยกตัวอย่าง เช่น การเปิดใช้งาน repository ที่กำหนดส่วนของ `[example]`, `[example-debuginfo]` และ `[example-source]` ให้พิมพ์ว่า :
```
~]# yum-config-manager --enable example\*
Loaded plugins: product-id, refresh-packagekit, subscription-manager
============================== repo: example ==============================
[example]
bandwidth = 0
base_persistdir = /var/lib/yum/repos/x86_64/6Server
baseurl = http://www.example.com/repo/6Server/x86_64/
cache = 0
cachedir = /var/cache/yum/x86_64/6Server/example
[output truncated]
```

เมื่อทำเสร็จ  `yum-config-manager --enable` จะแสดงการกำหนดค่าที่เป็นปัจจุบันของ repository

#### Disabling a Yum Repository
ถ้าต้องปิดใช้งาน Yum repository เราต้องเป็นยศ root แล้วพิมพ์คำสั่ง :

`yum-config-manager --disable repository`

ัวแปร *repository* ตรงคำสั่งเมิ่อกี้ จะเป็น unique ID ของ repository (ใช้คำสั่ง `yum repolist all` เพื่อลิสต์รหัส repository
ทั้งหมดที่มี) คล้ายกันกับ `yum-config-manager --enable` แล้วเราสามารถใช้ glob expression เพื่อปิดใช้งาน repository ทั้งหมดที่ตรงกันพร้อมๆ กันได้

`yum-config-manager --disable glob_expression`

เมื่อทำเสร็จ  `yum-config-manager --disable` จะแสดงการกำหนดค่าที่เป็นปัจจุบัน

### Creating a Yum Repository
ขั้นตอนการสร้าง Yum repository มีขั้นตอนดังนี้
1. ติดตั้งแพ็คเกจ **createrepo** (เราก็เป็นยศ root ถึงจะติดตั้งได้) \
  `yum install createrepo`
2. คัดลอกแพ็คเกจทั้งหมดทั้งที่เราอยากได้ใน repository เอาไปใส่ไว้ที่ directory เดียว เช่น `/mnt/local_repo/`
3. เปลี่ยนเป็น directory นี้ และรันคำสั่ง :
  `createrepo --database /mnt/local_repo`

ระบบจะทำการสร้าง metadata ที่จำเป็นสำหรับ Yum repository รวมถึง SQLite database เพื่อเพิ่มความเร็วในการทำงานของ `yum`

# References
- Installing and Managing Software : YUM<br>
  https://access.redhat.com/documentation/th-th/red_hat_enterprise_linux/7/html/system_administrators_guide/ch-yum#doc-wrapper
- What is Yum?<br>
  https://www.digitalocean.com/community/tutorials/what-is-yum
- How To Install "yum" Package on Ubuntu \
  https://zoomadmin.com/HowToInstall/UbuntuPackage/yum
- Configuring Yum and Yum Repositories \
  https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/sec-configuring_yum_and_yum_repositories

