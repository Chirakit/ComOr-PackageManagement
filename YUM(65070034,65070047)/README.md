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

