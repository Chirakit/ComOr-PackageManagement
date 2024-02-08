# Yellowdog Updater, Modified (YUM)

<hr>

## YUM คืออะไร

YUM คือ โปรแกรมจัดการ package ที่ใช้กันในหลายระบบปฏิบัติการ Linux ที่มีความนิยมเช่น Fedora และ CentOS. YUM เป็นอินเตอร์เฟซ (front-end) สำหรับตัวจัดการ package จรูปแบบ RPM ซึ่งหมายความว่ามันจัดการกับ package ที่มีรูปแบบไฟล์ .rpm

เหมือนกับ APT, YUM ทำงานผ่านการใช้งานของฐานข้อมูลซอฟต์แวร์หรือที่เรียกว่า "repositories" หรือ "repos" ซึ่งเป็น Directories พิเศษที่เก็บรวมแพคเกจซอฟต์แวร์ต่าง ๆ Repositories มักจะถูกเก็บบนเซิร์ฟเวอร์ระยะไกลที่ผู้ใช้สามารถเข้าถึงผ่านการเชื่อมต่อเครือข่ายได้ แต่ก็เป็นไปได้ที่ผู้ใช้จะเก็บแพคเกจซอฟต์แวร์ในรีพอสิทอรีบนเครื่องที่ตั้งอยู่ภายในเครื่องของตนเองได้

"YUM" เป็นคำย่อที่มีความหมายว่า "Yellowdog Updater, Modified" ชื่อนี้นำกลับมาจากต้นกำเนิดของ YUM ที่เป็นการเขียนใหม่ของ Yellowdog UPdater (หรือที่รู้จักกันว่า "YUP") ซึ่งเป็นโปรแกรมอัปเดตซอฟต์แวร์สำหรับระบบปฏิบัติการ Yellow Dog Linux ที่ปัจจุบันไม่มีการพัฒนาต่อแล้ว. การเขียนใหม่ของ YUM เองนั้นได้ชื่อว่า Dandified YUM หรือ "DNF" ที่ได้ทำการแทนที่ YUM เป็นตัวจัดการ package เริ่มต้นใน Fedora และ Red Hat Enterprise Linux ในปัจจุบัน

Yum เป็นตัวจัดการ package ของ Red Hat ที่สามารถสืบค้นข้อมูลเกี่ยวกับ package ที่มีให้ใช้, ดึงข้อมูล package จากที่เก็บ, ติดตั้งและถอนการติดตั้ง package , และอัปเดตระบบทั้งหมดไปยังเวอร์ชันล่าสุดที่มีให้. Yum ทำหน้าที่การแก้ไขข้อผิดพลาดขึ้นอัตโนมัติเมื่อมีการอัปเดต, ติดตั้ง, หรือถอนการติดตั้ง package, และดังนั้นสามารถกำหนด, ดึงข้อมูล, และติดตั้ง package ที่ต้องการทั้งหมดที่มีให้ใช้โดยอัตโนมัติได้

Yum สามารถกำหนดค่าเพิ่มเติมให้กับที่เก็บข้อมูล (repositories) หรือแหล่งข้อมูล package, และยังมีปลั๊กอินหลายตัวที่เพิ่มประสิทธิภาพและขยายความสามารถของ Yum. Yum สามารถทำงานในหลายภารกิจที่เหมือนกับ RPM ได้; นอกจากนี้, หลายตัวเลือกบนบรรทัดคำสั่งก็มีลักษณะเดียวกัน. Yum ทำให้การจัดการ package เป็นเรื่องที่ง่ายและไม่ซับซ้อนทั้งบนเครื่องเดียวหรือกลุ่มเครื่อง

Yum ยังช่วยให้คุณสามารถตั้งค่าที่เก็บข้อมูลของคุณเองที่มี package RPM เพื่อดาวน์โหลดและติดตั้งบนเครื่องอื่นได้อย่างง่ายดาย. เมื่อเป็นไปได้, yum ใช้การดาวน์โหลดพร้อมกันของ package และ metadata หลายรายการเพื่อเพิ่มความเร็วในการดาวน์โหลด

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
