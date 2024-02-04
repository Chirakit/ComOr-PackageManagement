### Debian
Dabian  เป็นชุดของซอฟต์แวร์เสรีที่พัฒนาโดยอาสาสมัครภายใต้โครงการเดเบียน ภายใต้โครงการนี้มี **เดเบียนลินุกซ์** (Debian GNU/Linux) ที่ใช้ลินุกซ์เป็นเคอร์เนล และใช้เครื่องมือต่าง ๆ ในโครงการ GNU ประกอบกันเป็นระบบปฏิบัติการ 

Dabian เป็นโปรเจ็กถูกเริ่มต้นโดย Ian Murdock ในวันที่ 16 สิงหาคม ค.ศ. 1993, รุ่นของเดเบียนนับรุ่น stable เป็นหลัก ปัจจุบันรุ่น stable ล่าสุดคือ 12 หรือ Bookworm โดยโค้ดเนมของแต่ละเวอร์ชันนั้นจะตั้งตามชื่อตัวละครจากเรื่อง ToyStory
<img src="images\Toy_Story_logo.png" alt="drawing" width="200"/>
#### Version History
- 1.1 – buzz, 17 มิถุนายน ค.ศ. 1996
- 1.2 – rex, 12 ธันวาคม ค.ศ. 1996
- 1.3 – bo, 2 มิถุนายน ค.ศ. 1997
- 2.0 – hamm, 24 กรกฎาคม ค.ศ. 1998
- 2.1 – slink, 9 มีนาคม ค.ศ. 1999
- 2.2 – potato, 15 สิงหาคม ค.ศ. 2000
- 3.0 – woody, 19 กรกฎาคม ค.ศ. 2002
- 3.1 – sarge, 6 มิถุนายน ค.ศ. 2005
- 4.0 – etch, 8 เมษายน ค.ศ. 2007
- 5.0 – lenny, 14 กุมภาพันธ์ ค.ศ. 2009
- 6.0 – squeeze, 6 กุมภาพันธ์ ค.ศ. 2011
- 7 – wheezy, 4 พฤษภาคม ค.ศ. 2013
- 8 – jessie, 26 เมษายน ค.ศ. 2015
- 9 – stretch, 17 มิถุนายน ค.ศ. 2017
- 10 – Buster, 6 กรกฎาคม ค.ศ. 2019
- 11 – Bullseye, 14 สิงหาคม ค.ศ. 2021
- 12 - Bookworm, 10 มิถุนายน ค.ศ. 2023

#### Dabian Package Manager (`dpkr`)

`dprk` คือ package manager ของระบบที่ใช้ Debian ตัวคอมแมน `dpkg` มีหน้าที่รองรับรายละเอียดระดับต่ำของ package management เช่น การ `unpack` และ `install` packages, จัดการ `config` ของ packages, และ ดูแล database ของ package ที่ลงไว้ โดยปกติ `dpkg` จะถูกใช้ร่วมกับ package management tools ตัวอื่นๆ เช่น apt ที่จะมีระดับ interface ที่สูงกว่าระบบ dpkg

#### Syntax

`dpkg [options] <action> <package_name>`
- -i − Install a package.
- -r − Remove a package.
- -P − Purge a package (remove package and configuration files).
- -l − List all installed packages.
- -s − Show information about a package.
- -S − Search for a package by file name.
- -L − List files installed by a package.

##### Installing a package
