# Launch Splunk Instance On AWS
1. Login AWS Console
![](../images/1.1.jpg)
2. Enter EC2 Console
![](../images/1.2.jpg)
3. Click "Launch Instance"
![](../images/1.3.jpg)
4. Type "splunk" in the search box and Choose "Splunk Enterprise" in "AWS Marketplace"
![](../images/1.4.jpg)
![](../images/1.5.jpg)
5. 

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::xxxxxx/*"
        }
    ]
}
```
![](../images/01-02.jpg)
20. Click "Save"
15. Access Static website hosting Endpoint Again
16. The Website can display normally now
![](../images/01-04.jpg)