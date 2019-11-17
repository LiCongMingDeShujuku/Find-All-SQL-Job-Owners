![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 查找所有SQL作业的所有者
#### Find All SQL Job Owners
**发布-日期: 2015年12月09日 (评论)**

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这里是一些可以用来返回到所有作业所有者的快速SQL逻辑（logic）。

## English
Here’s some quick SQL logic to return all the Job Owners.

---
## Logic
```SQL
use master;
set nocount on
 
if object_id('tempdb..#job_owners') is not null
drop table  #job_owners
create table    #job_owners
(
server_name varchar(255)
,   job_owner_name  varchar(255)
,   job_name varchar(255)
,   date_created    datetime
)
insert into #job_owners
select
'server_name' = @@servername
,   'job_owner_name'    = upper(suser_sname(owner_sid))
,   'job_name' = upper(sj.name)
,   'date_created' = date_created
from
msdb..sysjobs sj
 
select
server_name
,   job_owner_name
,   job_name
,   'date_created' = left(date_created, 12) + ' ' + datename(dw, date_created) from
#job_owners
order by
date_created
,   job_name asc
 
drop table #job_owners
```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

