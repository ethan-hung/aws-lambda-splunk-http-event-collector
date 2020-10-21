# Set Splunk HTTP event Collector
1. Login Splunk and Click "Settings->Data inputs"
![](../images/3.1.jpg)
2. Click "HTTP Event Collector"
![](../images/3.2.jpg)
3. Click "Global Settings"
![](../images/3.3.jpg)
4. Edit Global Settings
* All Tokens : Enabled
* Enable SSL : false
![](../images/3.4.jpg)
5. Click "New Token"
6. Type 
* Name : `your collector name`  
![](../images/3.6.jpg)  
* App Context : `Search & Reporting (search)`  
![](../images/3.7.jpg)  
Click "Review" -> "Summit"  
![](../images/3.9.jpg)
7. New you have a splunk token for lambda
![](../images/3.10.jpg)
8. You can try this token
```ssh
curl -k  http://splunk-ip:8088/services/collector -H "Authorization:Splunk splunk-hec-token" -d "{\"sourcetype\":  \"trial\",\"event\":\"hello world!\"}"

-- For example
curl -k  http://13.113.194.6:8088/services/collector -H "Authorization:Splunk 572a98bb-36f9-4240-9774-b9743cd4467a" -d "{\"sourcetype\":  \"trial\",\"event\":\"hello world!\"}"
```
![](../images/3.11.jpg)
![](../images/3.12.jpg)
