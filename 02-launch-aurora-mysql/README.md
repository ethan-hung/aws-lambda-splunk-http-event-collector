# Launch Aurora MySQL
1. Enter RDS Console  
![](../images/2.2.jpg)  
2. Click "Parameter groups" and Click "Create parameter group"  
![](../images/2.3.jpg)  
3. Parameter group detail  
* Parameter group family : aurora-mysql5.7  
* Type : DB Cluster Parameter Group  
* Group name : `your group name`  
![](../images/2.4.jpg)  
4. Click New Parameter group and change parameters  
* slow_query_log = 1  
![](../images/2.5.jpg)  
* general_log = 1  
![](../images/2.6.jpg)  
* long_query_time = 0.1 (100ms)  
![](../images/2.7.jpg)  
* log_queries_not_using_indexes = 1  
![](../images/2.8.jpg)  
* log_output = FILE  
![](../images/2.9.jpg)  
* server_audit_logging = 1  
![](../images/2.10.jpg)  
* server_audit_events = CONNECT,QUERY,QUERY_DCL,QUERY_DDL,QUERY_DML,TABLE  

| Event     | Description                                                                      |
| --------- | -------------------------------------------------------------------------------- |
| CONNECT   | 記錄成功與失敗連線，還有中斷連線。此事件包含使用者資訊                           |
| QUERY     | 以純文字記錄所有查詢，包括因為語法或許可錯誤而失敗的查詢                         |
| QUERY_DCL | 類似於 QUERY 事件，但只傳回資料控制語言 (DCL) 查詢 (GRANT、REVOKE 等)            |
| QUERY_DDL | 類似於 QUERY 事件，但只傳回資料定義語言 (DDL) 查詢 (CREATE、ALTER 等)            |
| QUERY_DML | 類似於 QUERY 事件，但只傳回資料操作語言 (DML) 查詢 (INSERT、UPDATE 和 SELECT 等) |
| TABLE     | 記錄因為執行查詢而受影響的資料表                                                 |

![](../images/2.11.jpg)  
1. Click "Databases" and Click "Create database"  
![](../images/2.12.jpg)  
6. Choose Engine type  
* Engine type : Amazon Aurora  
* Edition : Amazon Aurora with MySQL compatibility  
* Capacity : Provisioned  
* Version : Aurora (MySQL 5.7) 2.09.0  
![](../images/2.13.jpg)  
* Templates : Dev/Test  
* DB instance class : Burstable classes (includes t classes)  
* DB instance type : db.t2.small  
* Multi-AZ deployment : Don't create an Aurora Replica  
![](../images/2.15.jpg)  
* Additional configuration  
* DB cluster parameter group : `your parameter group name`  
![](../images/2.16.jpg)  
* Log Exports : Audit log, Error log, General log, Slow query log  
![](../images/2.20.jpg)  
Click "Create database"  
7. Wait for the database status to be available  
![](../images/2.17.jpg)  
You can see MySQL Logs in the AWS Cloudwatch Logs  
![](../images/2.18.jpg)  
![](../images/2.19.jpg)  