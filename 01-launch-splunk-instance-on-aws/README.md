# Launch Splunk Instance On AWS
1. Login AWS Console & Enter EC2 Console
2. Click "Launch Instance" and Type "splunk" in the search box and Choose "Splunk Enterprise" in "AWS Marketplace"
![](../images/1.4.jpg)
3. Splunk EC2 Instance Detail Setting
* Instance type : t2.micro
* Subnet : Public Subnet
* Storage : 20GB(GP2)
* Security Group : 
>> TCP 22 : Your IP
>> TCP 8000 : 0.0.0.0/0
    TCP 554 : 0.0.0.0/0
    TCP 8089 : 0.0.0.0/0
    TCP 9997 : 0.0.0.0/0
    TCP 443 : 0.0.0.0/0
    TCP 8088 : 0.0.0.0/0
![](../images/1.10.jpg)
4. wait Splunk Splunk Status is "running"
![](../images/1.11.jpg)
5. Now You can use the browser to open Splunk
![](../images/1.12.jpg)
6. Reset Splunk default password
```bash
ssh ec2-user@<splunk-instance-ip> -i keypair.pem
```
![](../images/1.13.jpg)
```bash
sudo su
cd /opt/splunk/etc
mv passwd passwd.old
cd /opt/splunk/etc/system/local
vim user-seed.conf
```
```
[user_info]
USERNAME = admin
PASSWORD = password
```
```
/opt/splunk/bin/splunk restart
```
