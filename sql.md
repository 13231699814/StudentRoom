#	用户对系统要求

##	用户部分

信息要求：

###	注册

- 普通用户注册
  - 账号
  - 密码
  - 权限-2
- 管理员注册
  - 权限-1

~~~sql
--管理员注册
insert into yonghub (zhanghao,mima,quanxian) value("12345","12345",1)
--学生注册
insert into yonghub (zhanghao,mima,quanxian) value("456789","456789",2)
~~~

###	登录

- 通过账号（学号）查询密码和权限

~~~sql
select 
mima,quanxian
from yonghub
where zhanghao = "12345"
~~~

###	查询学生信息

- 宿舍楼相关信息
  - 宿舍号
  - 楼号
  - 床位
- 学生信息
  - 学号
  - 姓名
  - 性别
  - 联系电话

~~~sql
select xueshengb.xuehao,xingming,xingbie,lianxidianhua,sushebianhao,louhao from xueshengb left join susheb
on xueshengb.xuehao = susheb.xuehao
~~~

###	提交查询报修信息

- 先添加报修表
- 再添加报修数据表

~~~sql
insert into baoxiub (tijiaoriqi,baoxiubianhao,xuehao) value("1980-06-19",'11113333','1201001001')
~~~

~~~sql
insert into baoxiushujvb (sushehao,wupinhao,baoxiuyuanyin,baoxiubianhao) value('01#201','01','坏了','11113333')
~~~

###	修改密码

- 登录之后
- 通过账号（学号）寻改密码

~~~sql
update 
yonghub
set mima = "456123"
where zhanghao = "12345"
~~~

##	管理员部分

###	登录

- 通过账号（学号）查询密码和权限

~~~sql
select 
mima,quanxian
from yonghub
where zhanghao = "12345"
~~~

###	查询学生信息

- 宿舍楼相关信息
  - 宿舍号
  - 楼号
  - 床位
- 学生信息
  - 学号
  - 姓名
  - 性别
  - 联系电话

~~~sql
select xueshengb.xuehao,xingming,xingbie,lianxidianhua,sushebianhao,louhao from xueshengb join susheb
on xueshengb.xuehao = susheb.xuehao
~~~

###	查询报修信息

~~~sql

select tijiaoriqi,baoxiub.sushehao,xuehao,wupinhao,baoxiuyuanyin,baoxiub.baoxiubianhao from baoxiub
left join baoxiushujvb
on baoxiub.baoxiubianhao = baoxiushujvb.baoxiubianhao
union
select tijiaoriqi,baoxiub.sushehao,xuehao,wupinhao,baoxiuyuanyin,baoxiub.baoxiubianhao  from baoxiub
right join baoxiushujvb
on baoxiub.baoxiubianhao = baoxiushujvb.baoxiubianhao

~~~

###	修改报修信息（添加结束日期）

~~~sql
update 
baoxiub
set jiejueriqi = "1980-06-19"
where xuehao = "1201001001"
~~~

###	删除报修信息

~~~sql
DELETE baoxiub,baoxiushujvb 
from baoxiub LEFT JOIN baoxiushujvb 
ON baoxiub.baoxiubianhao = baoxiushujvb.baoxiubianhao 
WHERE baoxiub.baoxiubianhao='1123123'
~~~

###	修改密码

- 登录之后
- 通过账号（学号）寻改密码

~~~sql
update 
yonghub
set mima = "456123"
where zhanghao = "12345"
~~~

### 查询访客信息

```sql
select 
xingming,lianxifangshi,mudi,fangkeb.zhengjianhao ,fangwenshijan,likaishijian from fangkeb
left join fangwenb
on fangwenb.zhengjianhao = fangkeb.zhengjianhao 
union
select 
xingming,lianxifangshi,mudi,fangkeb.zhengjianhao ,fangwenshijan,likaishijian from fangkeb
right join fangwenb
on fangwenb.zhengjianhao = fangkeb.zhengjianhao

```

### 修改访客离开时间

```sql
update 
fangwenb
set likaishijian = "2014-09-05"
where xuehao = "1201001001"

```

### 删除访客信息

```sql
DELETE fangkeb,fangwenb 
from fangkeb 
LEFT JOIN fangwenb 
ON fangkeb.zhengjianhao = fangwenb.zhengjianhao 
WHERE fangkeb.zhengjianhao='350428195012103566'
```

### 查询入住信息

```sql
SELECT 
ruzhushijian,likaishijian,sushehao,louhao,cengshu,susheleixing,kezhurenshu,ruzhub.xuehao
FROM ruzhub
LEFT JOIN susheb
ON ruzhub.xuehao=susheb.xuehao
UNION
SELECT 
ruzhushijian,likaishijian,sushehao,louhao,cengshu,susheleixing,kezhurenshu,ruzhub.xuehao
FROM ruzhub
RIGHT JOIN susheb
ON ruzhub.xuehao=susheb.xuehao
```

### 更改入住信息

```sql
UPDATE
ruzhub
SET sushehao='01#208' WHERE xuehao='1201001001'

```

### 删除入住信息

```sql
DELETE susheb,ruzhub
FROM ruzhub
LEFT JOIN susheb
ON susheb.xuehao=susheb.xuehao
WHERE ruzhub.xuehao='1201001001'
```

### 查询调整宿舍信息

```sql
SELECT 
xingming,xingbie,lianxidianhua,ruxueriqi,banjibianhao,shenqingbianhao,sushebianhao,xueshengb.xuehao
FROM xueshengb
LEFT JOIN tiaozhengb
on xueshengb.xuehao=tiaozhengb.xuehao
UNION
SELECT 
xingming,xingbie,lianxidianhua,ruxueriqi,banjibianhao,shenqingbianhao,sushebianhao,xueshengb.xuehao
FROM xueshengb
RIGHT JOIN tiaozhengb
on xueshengb.xuehao=tiaozhengb.xuehao
```

### 更新调整信息

```sql
UPDATE
tiaozhengb
SET sushebianhao ='01#202' WHERE xuehao='1201001001'
```

### 删除调整信息

```sql
DELETE tiaozhengb,xueshengb
from tiaozhengb
LEFT JOIN xueshengb
ON tiaozhengb.xuehao=xueshengb.xuehao
where tiaozhengb.xuehao='1201001001'
```

### 查询申请信息

```sql
select shenhebianhao,shenqingshijian,zhanghao,shenheshijian,shenhebianhao,shenheneirong,shenqingb.xuehao
from shenqingb
left join tiaozhengb 
on shenqingb.xuehao=tiaozhengb.xuehao
union 
select shenhebianhao,shenqingshijian,zhanghao,shenheshijian,shenhebianhao,shenheneirong,shenqingb.xuehao
from shenqingb
right join tiaozhengb 
on shenqingb.xuehao=tiaozhengb.xuehao
```

### 更新申请信息

```sql
update shenqingb
set shenheneirong='12345678' where xuehao= '1201001001'
```

### 删除申请消息

```sql
DELETE shenqingb,tiaozhengb
from shenqingb
LEFT JOIN tiaozhengb
ON tiaozhengb.xuehao=shenqingb.xuehao
where tiaozhengb.xuehao='1201001001'
```

### 管理员查询编辑表

```sql
select 
zengjiashijian,xiugaishijian,shanchushijian,sushehao,bianjibiao.zhanghao from bianjibiao
left join yonghub
on bianjibiao.zhanghao = yonghub.zhanghao
union
select 
zengjiashijian,xiugaishijian,shanchushijian,sushehao,bianjibiao.zhanghao from bianjibiao
right join yonghub
on bianjibiao.zhanghao = yonghub.hanghao
```

### 管理员更新编辑表

```sql
update 
bianjibiao
set xiugaishijian = "2014-09-05"
where zhanghao = "1101001001";
```

### 管理员删除编辑表

```sql
DELETE bianjibiao,yonghub 
from bianjibiao 
LEFT JOIN yonghub 
ON bianjibiao.zhanghao = yonghub.zhanghao 
WHERE bianjibiao.zhanghao='1101001002'
```

### 管理员删除申请内容

```sql
DELETE shenqingb,yonghub 
from shenqingb 
LEFT JOIN yonghub 
ON shenqingb.zhanghao = yonghub.zhanghao 
WHERE bianjibiao.zhanghao='1101001002'
```

### 管理员查询申请内容

```sql
select 
shenqingbianhao,shenqingshijian,xuehao,shenheshijian,shenhebianhao,shenqingjieguo from shenqingb
left join yonghub
on shenqingb.zhanghao = yonghub.zhanghao
union
select 
shenqingbianhao,shenqingshijian,xuehao,shenheshijian,shenhebianhao,shenqingjieguo from shenqingb
right join yonghub
on shenqingb.zhanghao = yonghub.zhanghao
```

### 管理员更新审核内容

```sql
update 
shenqingb
set shenheneirong = "98765432"
where zhanghao = "1101001007"
```

