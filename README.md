# Install-mysql-on-linux

# Description 💬

วิธี install mysql บน linux และ การ config เชื่อม database server และ การ set password

# Dependency ✋

resource : 

[How To Install MySQL on Ubuntu 20.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)

# Step 1 - Download & Install

update repo → install mysql-server → start service

```bash
# update package repository
sudo apt update

# Then install the mysql-server package
sudo apt install mysql-server

# Ensure that the server is running using the systemctl start command
sudo systemctl start mysql.service
```

# Step 2 - Config (password)

1. Open mysql prompt

```bash
sudo mysql
```

1. เปลี่ยน เป็น ค่า default password ให้ user root 

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

1. ออก

```bash
exit
```

จากนั้น ให้เรา ไป set การตั้งค่า server ของ mysql โดยใช้ คำสั่ง

```bash
sudo mysql_secure_installation
```

มันจะให้เรา set password ลง server แล่ะ แล้วจะ ขึ้น หน้า ประมาณนี้

```bash
Output
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

INPUT(1) : Press y|Y for Yes, any other key for No: Y

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

INPUT(2) : Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 0
```

มันจะเด้งมาให้เรา ใส่ตรงช่อง INPUT(1) ให้เรา พิมพ์ y ละกด enter
จากนั้นมันจะถามว่า ต้องการ password strong แค่ไหน ให้เรากรอกตรงช่อง INPUT(2) กรอกไปว่า 0

ซึ่งถ้าเราต้องการ password ให้ ก็ให้ใส่ แทนที่ ‘password’ เดิมที่เรา ตั้งไว้ตอนแรก ถ้าไม่อยากใช้ของเดิมก็กดข้ามไป

แล้วมันจะข้าม ไป set จิปาถะ กับ server ให้เรา พิมพ์ y รัวๆ จากนั้น ก็ออกจากระบบ แล้วลอง login เข้า mysql ใหม่

จะ login ก็ พิมพ์คำสั่งนี้ 

```bash
# -u : user , -p : password
mysql -u root -p
```

แล้วเดียวมันก็จะขึ้น เป็น prompt ของ mysql ให้เรา ใช้งาน

# Problem(1) : sudo mysql_secure_installation ❓

ถ้าข้างต้น ไม่ได้ ก็ลองมาทำตามอันนี้

พิมพ์ คำสั่ง แล้วมันจะเด้งไปให้เรา set account ใหม่ สำหรับ ตัว user root

```bash
sudo mysql_secure_installation
```

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled.png)

Enter : ใส่พาสเวิร์ดที่ได้ตั้งไว้ (ของ mysql นะเว้ย)
ถ้าใส่ แล้ว error ให้ลองใส่ เป็น : password
หรือไม่ก็ของตัว sudo ของเครื่อง linux : 1234

<aside>
💡 : หมายถึง ให้เรา input ค่าลงไป

</aside>

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%201.png)

Enter : y

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%202.png)

Enter : พาสเวิร์ด ใหม่ ที่อยากได้
Re-enter : ใส่อีกรอบ

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%203.png)

เขาถามว่า อยากได้ password ที่ มี ความปลอดภัยไหม ก็ตอบไปว่า : y

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%204.png)

เขาถามว่า remove user เก่า ที่ใช้ password เดิมนะ ก็ตอบไปว่า : y

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%205.png)

รองรับการทำ remote loging ไหม (login จาก ระยะไกล) ถ้าต้องการ ก็ : y ถ้าไม่ก็ : n

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%206.png)

ลบ test database และ จะทำ acces เข้าด้วย password ตัวใหม่นะ โอเค ถ้าใช่ ก็ : y

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%207.png)

reload สิทธิ์การเข้าถึง ใหม่นะ เว้ย เครบ่ อันนี้ให้ : y โล้ด

![Untitled](Install-mysql-on-linux%20d1a89d013668437bbd43736cd2551173/Untitled%208.png)

ถ้าขึ้นแบบนี้ ก็ ตั้ง password ให้ user root สำเร็จแล้ว 
login เข้า mysql ได้เลย ด้วยคำสั่ง

```bash
# -u : user , -p : password
mysql -u root -p
```

complete!

# Author ✍️

[zergreen - Overview](https://github.com/zergreen)