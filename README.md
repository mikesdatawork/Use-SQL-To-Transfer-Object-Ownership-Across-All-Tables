![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Transfer Object Ownership Across All Tables
**Post Date: September 19, 2016**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Suppose you're doing yet another database migration and find yourself again changing the Object Ownership aka Schema Ownership in the post 2012 world… Here's some quick logic to transfer all object ownership to DBO. Alternatively you can simply change 'dbo' to another name, but for the moment; we'll be using DBO in this example.</p>      


## SQL-Logic
```SQL
use mydatabase;
set nocount on
 
declare @set_new_schema  varchar(max)
set     @set_new_schema  = ''
select  @set_new_schema  = @set_new_schema +
'alter schema dbo transfer ' + table_schema + '.' + table_name + '';' char(10)
from information_schema.tables where table_schema = 'MyOldUserName'
 
exec    (@set_new_schema)
```

Next just run a quick query to confirm.
1	select table_schema, table_name from information_schema.tables order by table_schema asc
If you're looking to see whats statements are being run first; just run the following:


```SQL
set nocount on
 
declare @set_new_schema  varchar(max)
set     @set_new_schema  = ''
select  @set_new_schema  = @set_new_schema +
'alter schema dbo transfer ' + table_schema + '.' + table_name + '';' char(10)
from information_schema.tables where table_schema = 'MyOldUserName'
 
select    (@set_new_schema) for xml path(''), type
```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

    
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

