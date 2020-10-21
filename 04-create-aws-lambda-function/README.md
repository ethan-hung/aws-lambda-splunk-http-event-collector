# Launch Splunk Instance On AWS
1. Enter Lambda Console  and Click "Create function"  
![](../images/4.2.jpg)  
2. Choose "Use a blueprint"  
![](../images/4.3.jpg)  
3. Type `splunk` in the search box and choose "splunk-cloudwatch-logs-processor"  
![](../images/4.4.jpg)  
4. Lambda - Basic information  
* Function name : `your lambda name`  
* Execution role : Create a new role with basic Lambda permissions   
![](../images/4.5.jpg)  
5. Lambda - Cloudwatch Logs trigger  
* Log group : `your cloudwatch logs name`  
* Filter name : `your filter name`  
![](../images/4.6.jpg)  
6. Lambda - Environment variables  
* SPLUNK_HEC_URL : http://`splunk-ip`:8088/services/collector  
* SPLUNK_HEC_TOKEN : `splunk-http-hec-token`  
![](../images/4.7.jpg)  
7. Create function  
![](../images/4.8.jpg)  
8. Choose "Designer->CloudWatch Logs" and enable Cloudwatch Logs trigger  
![](../images/4.9.jpg)  
![](../images/4.10.jpg)  
9. Now you can watch Lambda logs and metrics and Splunk  
![](../images/4.11.jpg)  
![](../images/4.12.jpg)  
![](../images/4.13.jpg)  