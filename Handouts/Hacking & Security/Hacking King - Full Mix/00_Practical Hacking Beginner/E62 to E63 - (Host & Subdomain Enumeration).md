---
جلسه: 62to63
Date: 2024-07-21
Is Finished?: true
Practice Primary: true
Practice Secondary: 
Time: 25:00
tags:
  - CyberSecurity
  - hacking
Category: Cyber Security
banner: 
Home: "[[Table of Content - Hacking & Security]]"
Pervious Episode: "[[E58 to E61 - (Setup Hack The Box & Hack Some Machines)]]"
Next Episode: "[[E64 to E68 - (Web Hacking - Part 1)]]"
---
-------
## E62 to E63 - (Host & Subdomain Enumeration)
- [Dir Busting & V-Host Enumeration - E62](#Dir%20Busting%20&%20V-Host%20Enumeration%20-%20E62)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [Aim of Dir Busting & V-Host Enumeration](#Aim%20of%20Dir%20Busting%20&%20V-Host%20Enumeration)
		- [Tools for this Operations](#Tools%20for%20this%20Operations)
		- [Word Lists](#Word%20Lists)
		- [Dir Busting](#Dir%20Busting)
			- [Normal Dir Busting](#Normal%20Dir%20Busting)
			- [Specify Extension for Dir Busting](#Specify%20Extension%20for%20Dir%20Busting)
		- [V-Host Enumeration](#V-Host%20Enumeration)
			- [Whats V-Host & V-Host Enumeration?](#Whats%20V-Host%20&%20V-Host%20Enumeration?)
			- [V-Host Enumeration](#V-Host%20Enumeration)
	- [Practical Demo](#Practical%20Demo)
		- [Demo Description](#Demo%20Description)
		- [TASK 6 - 1.3. Practical GoBuster(Deploy # 1)](#TASK%206%20-%201.3.%20Practical%20GoBuster(Deploy%20#%201))
		- [TASK 6 with `FFUF`](#TASK%206%20with%20%60FFUF%60)
- [Sub-Domain Enumeration - Challenge Takeover on THM - E63](#Sub-Domain%20Enumeration%20-%20Challenge%20Takeover%20on%20THM%20-%20E63)
	- [Definition & Instruction](#Definition%20&%20Instruction)
	- [Practical Demo](#Practical%20Demo)
		- [Connect to THM Playground](#Connect%20to%20THM%20Playground)
		- [TASK 1 - Help Us](#TASK%201%20-%20Help%20Us)
****
### Dir Busting & V-Host Enumeration - E62
#### Definition & Instruction
##### Aim of Dir Busting & V-Host Enumeration
دو مبحث مهم در Web Hacking & Pentesting فرآیند های Dir Busting و V-Host Enumeration هستند که برای مقاصد زیر استفاده میشوند:
- از فرآیند Dir Busting برای یافتن دایرکتوری، صفحات و فایل های یک وب سرور استفاده میشود.
- از فرآیند V-Host Enumeration برای یافتن Sub Domain های یک وب سرور یا همان زیر دامنه ها استفاده میشود.
- *اسلاید*:
	- ![[Pasted image 20240720191509.png]]
##### Tools for this Operations
1. `GoBuster`
	1. ابزاری Open Source و رایگان که به زبان GO نوشته شده است و برای پیاده سازی حملات Brute forcing بر روی دایرکتوری ها و فایل های یک وب سرور استفاده میشود.
	2. این ابزار، ابتدا یک لیست از نام های ممکن و معروف دایرکتوری ها و فایل هایی که در وب سرور ها وجود دارند تولید میکند ویا اینکه از یک Wordlist آماده استفاده میکند.
	3. سپس فایل ها و دایرکتوری های وب سرور هدف را با این لیست میسنجد، اینکار را با پیاده سازی یک حمله Bruteforce با استفاده از Wordlist تعریف شده بر روی url وب سرور انجام میدهد. 
	4. هر دایرکتوری، فایل و یا صفحه ای که هم در لیست کلمه و هم در وب سرور تارگت وجود داشته باشد را برمیدارد و آنرا جز دایرکتوری ها و فایل های درون وب سرور لیست میکند.
	5. در آخر هم سعی میکند که به دایرکتوری ها و فایل های یافت شده در وب سرور نفوذ کند.
	6. این ابزار هم میتواند در حملات Dir Busting و هم در فرآیند V-Host Enumeration استفاده شود.
2. `FFUF`
	1. این ابزار هم مانند GoBuster کار میکند اما کار را با سرعت بیشتری انجام میدهد. در واقع میتوان گفت نمونه پر سرعت Gobuster میباشد.
3. Slide
	1. ![[Pasted image 20240720192414.png]]
##### Word Lists
- یکی دیگر از موارد مهم در VHost & Directory Brute Forcing لیست کلماتی است که برای حمله استفاده میکنیم. در واقع یک Wordlist مناسب باید از کلمات و عبارات رایجی که در نام های دایرکتوری ها و VHost ها استفاده میشود، تشکیل شود.
- `DirBuster Wordlists`
	- ابزار Dir Buster یکسری Wordlist بصورت پیشفرض برای انجام این حملات دارد که میتوانیم در دایکتوری زیر این لیست ها را مشاهده کنیم:
	- `ls /usr/share/wordlists/dirbuster/`
	- یکی از بهترین و همچنین سبک ترین این لیست ها `directory-list-2.3-medium.txt` میباشد.
- `Sec Lists`
	- یکی از مجموعه Wordlist های معروف و کامل است که میتوانیم بصورت کامند بر روی ماشین های لینوکسی آنرا نصب کنیم. 
	- `sudo apt install seclists`
	- همچنین میتوانیم با رجوع به صفحه گیت های ابزار فایل ZIP مجموعه را دانلود کنیم.
	- *اسلاید*:
		- ![[Pasted image 20240720193051.png]]
##### Dir Busting
###### Normal Dir Busting
برای پیاده سازی این فرآیند میتوانیم از هر دو ابزار `GoBuster` و `FFUF` استفاده کنیم.
- *GoBuster*
```sh
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
	![[Pasted image 20240720193724.png]]
- *FUFF*
```sh
ffuf -u http://10.10.10.10/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
	![[Pasted image 20240720193737.png]]
###### Specify Extension for Dir Busting
میتوانیم در حمله Dir Busting پسوند های خاصی را مشخص کنیم که فقط صفحات یا فایل هایی با این پسوند برای ما پیدا شود. برای اینکار باید در `GuBuster` از فلگ `x-`  و در `FFUF` از فلگ `e-`  استفاده کنیم.
	![[Pasted image 20240720194126.png]]
- *GoBuster*
```sh
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.html,.js,.css 
```
	![[Pasted image 20240720194116.png]]
- *FUFF*
```sh
ffuf -u http://10.10.10.10/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e .html,.js,.css,.conf
```
##### V-Host Enumeration
###### Whats V-Host Method & V-Host Enumeration?
- *Whats Virtual Host Method?*
	- در این متد یک وب سرور چندنی هاست مجازی را ارائه میدهد. در واقع یک دامنه اصلی وجود دارد که به هاست اصلی متصل است، همچنین چندین زیر دامنه نیز در همان وب سرور وجود دارد که هر کدام آیپی و یا پورت مخصوص خود ا دارد.
	- وب سرور با استفاده از این اطلاعات (آیپی و پورت هر sub domain)  مسیریابی را بین این Virtual Host ها انجام میدهد.
	- در واقع هر Sub Domain در وب سرور که آیپی یا پورت مخصوص خود را دارد به عنوان یک هاست مجازی V-Host شناخته میشود.
- *Whats V-Host Enumeration?*
	- از فرآیند V-Host Enumeration برای یافتن هاست های مجازی و یا همان زیر دامنه ها در یک وب سرور استفاده میشود. 
	- این فرآیند در فاز Reconnaissance(شناسایی) در عملیات Web hacking/Pentesting دسته بندی میشود.
	- در واقع Attacker در فرآیند V-Host Enumeration سعی میکند تمام V-Host های درون یک وب سرور را پیدا کند و سپس با بررسی تمام V-Host ها، آسیب پذیر ترین آنها را برای نفوذ خود انتخاب میکند.
- *Slide*:
	- ![[Pasted image 20240720195403.png]]
###### V-Host Enumeration 
این فرآیند را با استفاده از دو ابزار `GoBuster` و `FFUF` میتوانیم پیاده سازی کنیم.
- *GoBuster*
```sh
gobuster vhost -u http://example.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-5000.txt --append-domain
```
	![[Pasted image 20240720200017.png]]
- *FFUF*
```sh
ffuf -u http://example.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.txt -H "HOST:FUZZ.example.com"
```
	![[Pasted image 20240720200008.png]]
#### Practical Demo
##### Demo Description
برای تمرین این مبحث از آزمایشگاه `THM-Web Enumeration` استفاده میکنیم >>
- https://tryhackme.com/room/webenumerationv2
	- ![[Pasted image 20240720200326.png]]
- برای تمرین GoBuster به `TASK 6` میرویم.
##### TASK 6 - 1.3. Practical GoBuster(Deploy # 1)
0. *Pre-Requires*
	- ابتدا باید عبارت `10.10.4.18 webenum.thm` را در فایل `etc/hosts/` اضافه کنیم.
		- `echo "10.10.4.18 webenum.thm" >> /etc/hosts`
			- ![[Pasted image 20240720201037.png]]
		- `10.10.4.18` is Room machine IP 
			- ![[Pasted image 20240720201104.png]]
		- حال باید با وارد کردن http://webenum.thm در مرورگر صفحه آزمایشگاه ماشین باز میشود.
			- ![[Pasted image 20240720201411.png]]
	- سپس باید ابزار GoBuster را بر روی ماشین نصب کنیم.
		- `sudo apt install gobuster`
1. *Initialize Dir Busting Attack*
	1. ابتدا میخواهیم با استفاده از GoBuster حمله را انجام دهیم >>
		1. `gobuster dir -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt`
			1. ![[Pasted image 20240720201937.png]]
		2. با اجرای حمله متوجه میشویم که دایرکتوری های Images, public, css, js, Changes, VIDEO وجود دارد.
			1. ![[Pasted image 20240720202107.png]]
	2. سپس حمله را با استفاده از GoBuster برای یافتن فایل های `php, conf, js` انجام میدهیم >>
		1. `gobuster dir -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,conf,js -t 32`
			1. ![[Pasted image 20240720202503.png]]
		2. در این حمله هم متوجه شدیم که فایل های `changes.conf , bootstrap.js` در هاست تارگت وجود دارد. 
			1. ![[Pasted image 20240720202610.png]]
	3. حال باید دایرکتوری های موجود در وب سرور که یافتیم را یکی یکی امتحان و باز کنیم تا ببنیم فایل و یا محتویات بدرد بخوری در آن یافت میشود >>
		1. http://webenum.thm/changes => Page doesn't exists
		2. http://webenum.thm/public => Directory is Empty
			1. ![[Pasted image 20240720210609.png]]
		3. http://webenum.thm/VIDEO => `flag.php` is there
			1. ![[Pasted image 20240720210745.png]]
	4. حال که فلگ مرحله را یافتیم و باید آنرا باز کنیم و مقدار فلگ را کپی کنیم.
		1. http://webenum.thm/VIDEO/flag.php
			1. ![[Pasted image 20240720210906.png]]
2. *Initialize V-Host Enumeration*
	1. در مرحله بعدی باید V-Host های موجود در وب سرور را پیدا کنیم. برای اینکار هم از Gobuster استفاده میکنیم.
	2. `gobuster vhost -u http://webenum.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.txt --append-domain`
		1. ![[Pasted image 20240720211732.png]]
		2. ![[Pasted image 20240720211744.png]]
	3. در این اسکن حمله متوجه شدیم که دو زیر دامنه زیر دامنه(V-Host) در وب سرور تارگت وجود وارد >>
		1. http://learning.webenum.thm
		2. http://products.webenum.thm
			1. ![[Pasted image 20240720211936.png]]
	4. حال باید این Sub Domain ها همان V-Host ها را نیز به فایل `etc/hosts/` اضافه کنیم تا بتوانیم آنها را در مرورگر مشاهده کنیم >>
		1. `sudo nano /etc/hosts`
			1. ![[Pasted image 20240720212417.png]]
		2. حال میتوانیم در مرورگر با وارد کردن آدرس زیر دامنه ها صفحه آنها را مشاهده کنیم.
		3. http://learning.webenum.thm
			1. ![[Pasted image 20240720212533.png]]
		4. http://products.webenum.thm
			1. ![[Pasted image 20240720212722.png]]
3. *Directory Brute Forcing for find flag*
	1. حال باید آخرین فلگ مرحله را نیز پیدا کنیم. برای اینکار با استفاده از Gobuster حمله ای Brute Force را برای یافتن تمام فایل های txt در هر دو Sub Domain این وب سرور پیاده سازی میکنیم.
	2. `gobuster dir -u http://learning.webenum.thm -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -x txt`
		1. ![[Pasted image 20240720213300.png]]
	3. `gobuster dir -u http://products.webenum.thm -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -x txt`
		1. در این حمله فایل `flag.txt` را میتوانیم مشاهده کنیم و کافیست آنرا در مرورگر باز کنیم تا محتویات فلگ را کپی کنیم و در جواب سوال آخر بنویسیم.
			1. ![[Pasted image 20240720213446.png]]
		2. http://products.webenum.thm/flag.txt
			1. ![[Pasted image 20240720213529.png]]
4. *TASK 6 Q_&_A*
	1. Run directory scan on host. other than css, images and js directories, What other directory available? `public, changes, video`
	2. Run directory scan on the host, in the CHANGES Directory whats files extension exists? `conf,js`
	3. Find flag by directory scanning.(in VIDEO directory) `thm{n1c3_w0rk}`
	4. There are some virtual host running on this host. What are they? `learning, products`
	5. Find Another flag in a virtual host. `thm{gobuster_is_fun}`
	6. Image of All Questions
		1. ![[Pasted image 20240720213635.png]]
-----
```sh
#0. Pre-Requires
echo "10.10.4.18 webenum.thm" >> /etc/hosts
sudo apt-get install gobuster
#1. Initialize Dir Busting
gobuster dir -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt

gobuster dir -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,conf,js -t 32

#2. Initialize V-Host Enumeration
gobuster vhost -u http://webenum.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.txt --append-domain
#3. Directory Brute Forcing for find flag
gobuster dir -u http://learning.webenum.thm -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -x txt 
```
##### TASK 6 with `FFUF`
0. *Dir Busting with `FFUF`*
	1. Normal Dir Busting
		1. `ffuf -u http://webenum.thm/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt`
			1. ![[Pasted image 20240720213957.png]]
			2. ![[Pasted image 20240720214040.png]]
	2. Dir Busting with Specify Extension
		1. `ffuf -u http://webenum.thm/Changes/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -e .html,.conf,.js`
			2. ![[Pasted image 20240720214408.png]]
1. *V-Host Enumeration with `FUFF`*
	1. اگر این اسکن را به شکل زیر و بدون تعریف یا فیلتر سایز و یا تعداد کلمات انجام دهیم، تعداد زیادی فایل واکشی میشود که فایل های بدر نخور هستند که باید فیلتر شوند >>
		1. `ffuf -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.txt -H "HOST:FUZZ.webenum.thm"`
			1. ![[Pasted image 20240720214902.png]]
	2. بنابراین پیشنهاد میشود با استفاده از `fw-`  تعداد کلمات را مشخص کنیم و یا با `fs-` سایز فایل ها را محدود کنیم تا نتیجه جستجو Filter شود. این تعداد در هر سناریو متفاوت است مثلا در اینجا فایل های بدرد نخور 205 کلمه دارند بنابراین میتوانیم از این تعداد استفاده کنیم >>
		1. `ffuf -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.txt -H "HOST:FUZZ.webenum.thm" -fw 205`
			1. ![[Pasted image 20240720215256.png]]
2. *Find any txt file(flag.txt in this scenario) in Target V-Hosts with `FFUF`*
	1. `ffuf -u http://products.webenum.thm/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -e .txt`
		1. ![[Pasted image 20240720215604.png]]
	2. میتوانیم مشاهده کنیم که فایل `flag.txt` در ماشین تارگت یافت شد.
		1. ![[Pasted image 20240720215700.png]]
-----
```sh
#0. Dir Busting with FFUF
ffuf -u http://webenum.thm/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt

ffuf -u http://webenum.thm/Changes/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -e .html,.conf,.js
#1. V-Host Enumeration with `FUFF`
ffuf -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.tx -H "HOST:FUZZ.webenum.thm"

ffuf -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1milion-20000.tx -H "HOST:FUZZ.webenum.thm" -fw 205
#2. Find any txt file(flag.txt in this scenario) in Target V-Hosts with `FFUF`
ffuf -u http://products.webenum.thm/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -e .txt
```
### Sub-Domain Enumeration - Challenge Takeover on THM - E63
#### Definition & Instruction
- در این جلسه میخواهیم به Sub Domain Enumeration بپردازیم و اینکار را در آزمایشگاه THM و روم بنام `Takeover` انجام میدهیم.
- https://tryhackme.com/room/takeover
	- ![[Pasted image 20240721191206.png]]
وظیفه این روم بسیار واضح است، در واقع باید Enumeration بر روی Domain تارگت انجام دهیم و تمام Sub Domain ها را بیابیم و سپس فلگ مرحله را در این زیر دامنه ها پیدا کنیم. این Room یک Task دارد و وارد کردن مقدار فلگ است. 
	![[Pasted image 20240721191822.png]]
#### Practical Demo
##### Connect to THM Playground
1. Click on `Access Machine` and Select `OpenVPN` and Download Configuration file
	1. ![[Pasted image 20240721191933.png]]
	2. ![[Pasted image 20240721192030.png]]
2. Now open terminal in downloaded folder in kali machine and run following command to connect THM playground
	1. `sudo openvpn davoodya.ovpn`
		1. ![[Pasted image 20240721192217.png]]
	2. `ifconfig` now *tun0* added to interfaces list.
		1. ![[Pasted image 20240721192907.png]]
3. Back to Takeover Room Page and TASK 1 => `Start Machine`
##### TASK 1 - Help Us
0. *Pre-Requires*
	1. `Start Machine` & Copy Takeover IP
	2. Ping Takeover IP from Kali to check connection
		1. ![[Pasted image 20240721193040.png]]
	3. Install SecLists => `sudo apt install seclists`
	4. Add domain name and machine ip in `/etc/hosts` 
		1. `nano /etc/hosts` Add below line to file
		2. `10.10.7.78 futurevera.thm`
			1. ![[Pasted image 20240721193716.png]]
		3. Now can open https://futurevera.thm on Browser
			1. ![[Pasted image 20240721194110.png]]
1. *Start Scanning*
	1. `sudo nmap -T5 -sS -sV -O 10.10.7.78` 
		1. `-sS` Stealth Scan
		2. `-sV` Version Scan
		3. `-O` OS Enumeration
	2. Scan Results =>
		1. پورت های `22, 80, 433 >> TCP` در ماشین تارگت باز هستند.
			1. ![[Pasted image 20240721193930.png]]
2. *Sub Domain Brute Forcing with `Gobuster`*
	1. اولین حمله را برای ورژن https انجام میدهیم >>
	2. `gobuster vhost -u https://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -k --append-domain`
		1. ![[Pasted image 20240721194519.png]]
	3. در این حمله دو زیر دامنه زیر در دامنه اصلی پیدا شد >>
		1. https://blog.futurevera.thm
		2. https://support.futurevera.thm
	4. انجام حمله برای ورژن http >>
		1. `gobuster vhost -u https://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -k --append-domain`
			1. ![[Pasted image 20240723233225.png]]
		2. در نتیجه این حمله هم دو زیر دامنه http://portal.futurevera.thm و http://payroll.futurevera.thm در هاست تارگت یافت شد.
4. *Sub Domain Brute Forcing with `FFUF`*
	1. اگر اسکن را بدون `fs-` انجام دهیم تعداد زیادی فایل به عنوان زیر دامنه شناخته میشوند که بدرد ما نمیخورد، به همین خاطر نتیجه اسکن را بر اساس سایز فیلتر میکنیم:
		1. `ffuf -u https://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subsubdomains-top1million-20000.txt -H "Host:FUZZ.futurevera.thm" -fs 4605`
			1. ![[Pasted image 20240721195147.png]]
	2. در نتیجه اسکن دو زیر دامنه https://blog.futurevera.thm و https://support.futurevera.thm پیدا شد:
		1. ![[Pasted image 20240721194957.png]]
	3. همین حمله را برای ورژن `http` وبسایت هم انجام میدهیم:
	4. `ffuf -u http://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -H "Host:FUZZ.futurevera.thm" -fs 0`
		1. ![[Pasted image 20240721195310.png]]
	5. در نتیجه این حمله هم دو زیر دامنه http://portal.futurevera.thm و http://payroll.futurevera.thm در هاست تارگت یافت شد:
		1. ![[Pasted image 20240721195439.png]]
5. *Add Sub Domains to `/etc/hosts`*
	1. `nano /etc/hosts` Add below line to file
	2. `10.10.7.78 futurevera.thm https://blog.futurevera.thm https://support.futurevera.thm`
		1. ![[Pasted image 20240721195751.png]]
	3. Now Open https://blog.futurevera.thm
		1. ![[Pasted image 20240721195910.png]]
	4. اولین کار که پس از رفتن به این URL باید انجام دهیم بررسی Certificate آن وبسایت است. در اینجا هم این مجوز را بررسی میکنیم تا ببینیم فلگ درون آن است و یا خیر >>
		1. برای اینکار ابتدا بر روی قفل بقل URL کلیک میکنیم:
			1. ![[Pasted image 20240721200046.png]]
		2. سپس به تب `Security` میرویم و بر روی `View Certificate` کلیک میکنیم:
			1. ![[Pasted image 20240721200134.png]]
		3. حال محتویات Certificate را بررسی میکنیم که ببینیم Flag در متن هست یا خیر 
			1. ![[Pasted image 20240721200219.png]]
	5. Now Open https://support.futurevera.thm
	6. حال باید Certificate این دامنه را هم بررسی کنیم >>
		1. در بررسی `Certificate` در فیلد `DNS Name` میتوانیم یک زیر دامنه اضافه دیگری را مشاهده کنیم که مقدار آنرا کپی میکنیم.:
			1. ![[Pasted image 20240721200416.png]]
6. *Get TASK Flag*
	1. دامنه مورد نظر را از فیلد `DNS Name` کپی میکنیم و باید آنرا را در فایل `etc/hosts` در مقابل آیپی ماشین وارد کنیم.
	2. حال کافیست URL را در مروگر باز کنیم تا در هنگام واکشی صفحه مقدار  فلگ را در URL مشاهده کنیم:
		1. ![[Pasted image 20240721200905.png]]
	4. *مقدار فلگ*:
		1. `flag{beeaOd6edfcee06a59b83fb50ae81b2f}.`
			1. ![[Pasted image 20240721201243.png]]
7. Room Completed
-----
```sh
#0. Pre-Requires
sudo openvpn davoodya.ovpn
sudo apt install seclists
ping 10.10.7.78
nano /etc/hosts #Add below line to file
	"10.10.7.78 futurevera.thm"
#1. Start Scanning
sudo nmap -T5 -sS -sV -O 10.10.7.78
#2. Sub Domain Brute Forcing with Gobuster
gobuster vhost -u https://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -k --append-domain
#3. Sub Domain Brute Forcing with FFUF
ffuf -u https://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -H "Host:FUZZ.futurevera.thm" -fs 4605
#find 'HTTP' sub domains 
ffuf -u http://futurevera.thm -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -H "Host:FUZZ.futurevera.thm" -fs 0
#4. Add Sub Domains to `/etc/hosts`
nano /etc/hosts #add below lines to file
	"10.10.7.78 futurevera.thm https://blog.futurevera.thm https://support.futurevera.thm"
#5. Get TASK Flag
"Open Browser and goto https://blog.futurevera.thm
Now goto website Certificate and Copy additional Sub Domain in DNS Field
goto additional subdomain and get flag"
```
### !