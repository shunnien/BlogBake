---
layout: post
title: 'Sql Server 取得所有欄位定義'
date: 2015-10-22 04:11
comments: true
categories: [sql, SQLServer]
---
把一些以前整理的東西，紀錄一下

此部分最好在 Sql Server 2005 以上使用， Sql Server 2000 就沒使用過

```
SELECT
CASE  a.TABLE_TYPE
WHEN  'BASE TABLE'  THEN '資料表'
WHEN 'VIEW'  THEN '檢視表'
END as 表格類型 ,
    a.TABLE_NAME                as 表格名稱,
    b.COLUMN_NAME               as 欄位名稱,
    b.DATA_TYPE                 as 資料型別,
    b.CHARACTER_MAXIMUM_LENGTH  as 最大長度,
    b.COLUMN_DEFAULT            as 預設值,
    b.IS_NULLABLE               as 允許空值,
    (
        SELECT
            value
        FROM
            fn_listextendedproperty (NULL, 'schema', 'dbo', 'table', 
                                     a.TABLE_NAME, 'column', default)
        WHERE
            name='MS_Description' 
            and objtype='COLUMN' 
            and objname Collate Chinese_Taiwan_Stroke_CI_AS=b.COLUMN_NAME
    ) as 欄位備註
FROM
    INFORMATION_SCHEMA.TABLES  a
    LEFT JOIN INFORMATION_SCHEMA.COLUMNS b ON (a.TABLE_NAME=b.TABLE_NAME)
--WHERE
--    TABLE_TYPE='VIEW'
--    TABLE_TYPE='BASE TABLE'
ORDER BY
   a.TABLE_TYPE, a.TABLE_NAME, ordinal_position
```