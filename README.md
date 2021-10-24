# CSF-LDF-WHM
HOW TO INSTALL CSF AND LDF WITH WHM/cPanel

Steps on how to download and install CSF and LDF with the WHM interface. Also, the last command will remove APF and BFD, which are the same type of application, so there are no conflicts over the iptables they control.

NSTALL CODE
 

cd /tmp

rm -fv csf.tgz

wget https://download.configserver.com/csf.tgz

tar -xzf csf.tgz

cd csf

sh install.sh

sh /etc/csf/remove_apf_bfd.sh

 

POST INSTALL STEPS
After a successful install, open WHM and proceed to the Plugins -> ConfigServer Security & Firewall page

Click Configure Firewall and set the value of TESTING to 0

On VPS packages, also set MONOLITHIC_KERNEL to 1

Scroll down and press Change

Click Restart csf+ldf

Back on the main ConfigServer Security & Firewall page, the Quick Allow option can be used to add an IP to the Allow table to prevent being blocked in the event of inadvertent login failures from a trusted IP address.

TROUBLESHOOTING

ERROR

iptables LKM ip_tables missing so this firewall cannot function unless you enable MONOLITHIC_KERNEL in /etc/csf/csf.conf AND/OR you receive emails from the server saying lfd failed....A restart was attempted automagically

 

SOLUTION

In WHM, go to ConfigServer Security & Firewall and then click the Configure Firewall button. Scroll down to MONOLITHIC_KERNEL and set the value to 1 to enable it. Then press the Change button, followed by the Restart csf+ldf button on the next page.

OR connect via SSH and edit /etc/csf/csf.conf Then, change from MONOLITHIC_KERNEL = 0 to MONOLITHIC_KERNEL = 1 and save the file and restart the server with

 

csf -r

OTHER NOTES

The Check Server Security can be used as a base level tool to grade and recommend security items on the web server

To uninstall CSF use

 

sh /etc/csf/uninstall.sh


---- Recommend Actions ------

php.ini
disable_functions = show_source, system, shell_exec, passthru, exec, popen, proc_open

Enable BoxTrapper spam trap = disabled
