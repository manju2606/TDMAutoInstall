Important File Extension Renames:
Change all "*.ps1.txt" to "*.ps1"
Change all "*.lnk.txt" to "*.lnk"
Change all "*.bat.txt" to "*.bat"

Important:
This installer uses two GA files.
TDM Repository 3.2.12 (GA) = GEN500000000001739.zip
TDM Server 4.6 (GA) = GEN500000000001752.zip

Important:
1) Folder used for this install Example: "C:\TEMP\TDM-Auto-Install"  (Change the scripts if different)
2) Extract TDM Repository folder and files to "C:\TEMP\TDM-Auto-Install\CATDM-DBInstaller-46"
3) Extract TDM Server files to "C:\TEMP\TDM-Auto-Install"

File to be updated under "C:\TEMP\TDM-Auto-Install"
auto_install_credentials.ps1 
portal_install_oracle.params 
portal_install_sqlserver.params
VM.properties



edit common_functions.ps1 (line 206)  Add AppDIR=c:\$name
  $argList = "/quiet","/L*V $log","APPDIR=c:\$name" 
  
 edit common_functions.ps1 (line 191 to 198)  
 comment out 
    #commonCreateDb gtrep
    #commonCreateDb creditcard
    #commonCreateDb creditcard_e
    #commonCreateDb travel
    #commonCreateDb travel_e
    #commonCreateDb orders
    #commonCreateDb orders_e
    #commonCreateDb scramble

To use this auto local install you need to:

0) Make sure that powershell version 3 or above is installed ( command $PSVersionTable.PSVersion)

1) Obtain the DB-Installer kit you want installed. If in a zip then extract it to CATDM-DBInstaller-* in this directory (the * being version). It only needs the ca-tdm-db-install-kit sub-directory.
2) Obtain the Portal installer you want installed. If in a zip extract the exe to this directory.
3) If you want to install GTServer then obtain the version that you want installed. If in a zip extract the exe to this directory.
4) Edit VM.properties and set:
	install_local = true
5) If you don't want to install GTServer then edit VM.properties and set:
	skip_gtserver_install = true
6) Start a command-prompt to run as administrator, CD to this directory and execute auto_local.bat.

If the auto install fails, remove the icon from the desktop and remove the sub-directory created for the failed step(s) (check auto_install.log) from this directory. Address the problem (usually missing files) and run again.

if DB-Installer kit install fails then remove Repo_Kit_Auto_Installed folder as well as the 'Auto Install Failed' link from the desktop. check auto_install.log for cause

if GT server install fails then check log files under GTServer_Auto_Installed folder as well as auto_install.log.  
To restart the GT Server install, make sure that 'Auto Install Failed' link (from the desktop) and GTServer_Auto_Installed folder are removed .

if Portal install fails then check installer log file under TDMPortal_Auto_Installed folder as well as auto_install.log.  
To restart the Portal install, make sure that 'Auto Install Failed' link (from the desktop) and TDMPortal_Auto_Installed folder are removed .
