# Appendix 01 Aurora MySQL
1. Max Connection
In Parameter Group [Link](https://docs.aws.amazon.com/zh_tw/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Performance.html)  

| Instances type | Max connections default value |
| -------------- | ----------------------------- |
| db.t2.small    | 45                            |
| db.t2.medium   | 90                            |
| db.t3.small    | 45                            |
| db.t3.medium   | 90                            |
| db.r5.large    | 1000                          |
| db.r5.xlarge   | 2000                          |
| db.r5.2xlarge  | 3000                          |

2. Connection fail
- Audit Log
```
2020-10-23T07:13:26.298081Z 34 [Note] Access denied for user 'admin'@'58.182.98.237' (using password: YES)
```

3. Create database
- SQL
```sql
create database mysqldemo;
```

- Audit Log
```
1603438736650167,database-1-instance-1,admin,1.34.6.81,30,964317,QUERY,world,'create database mysqldemo',0
```

- General Log
```
2020-10-23T07:38:56.637123Z 30 Query create database mysqldemo
```

4. Create Table
- SQL
```sql
CREATE TABLE customers (
  C_Id INT,
  Name varchar(50),
  Address varchar(255),
  Phone varchar(20)
);
```
- General Log
```
2020-10-23T07:47:31.319556Z   30 Query	CREATE TABLE customers (
  C_Id INT,
  Name varchar(50),
  Address varchar(255),
  Phone varchar(20)
)
```

- Audit Log
```
1603439251354761,database-1-instance-1,admin,1.34.6.81,30,966941,CREATE,world,customers,
```
```
1603439251360772,database-1-instance-1,admin,1.34.6.81,30,966941,QUERY,world,'CREATE TABLE customers (   C_Id INT,   Name varchar(50),   Address varchar(255),   Phone varchar(20) )',0
```

5. 