## Project_work_获取jx_bonus_formular Beta 1.0


1. 假设客户的数据库市本地连结，数据库假设是mssql 
2. 本专案建立在 [Project_work_获取數據与导出excel 1.0](https://github.com/smopthy/project_access_db_parameter)
3. beta 1.0 初期建立获取与资料清洁，後续完善回写数据库、导出excel 表
4. 利用正则表达获取中文字

## 导入基本数据package 

import pandas as pd 
import pyodbc 
import re

## 建立与数据库连接
```
    conn = pyodbc.connect(  
        'Driver={SQL Server Native Client 10.0};'  
        'Server=.;'  
        'Database=gshm_jx;'  
        'Trusted_Connection=yes;'  
    )  

    #{SQL Server Native Client 10.0} => mssql2008  
```

## 数据处理与清洗
```
    df_formular['formular']   
    df_formular_text = df_formular['formular'].iloc[590]  
```
## 正则表达获取中文字 并且 回写 sql query 的结果
```  
    text = re.sub("[A-Za-z0-9\!\%\[\]\,\。\+\-\*\)\(]", " ", df_formular_text).split(' ')

    for i in range(number):  
    df_parameter_pd = df_parameter[df_parameter['parameter_name'] == text[i]]  
    df_formula_name = text[i]  
    df_formula_name  
    if df_formula_name == ''or df_formula_name == '.':  
        pass   
    else :  
        df_formula_value = df_parameter_pd['para_value'].iloc[0]  
        df_formular_text = df_formular_text.replace(df_formula_name, str(df_formula_value))  

```

##　計算公式結果(函數 eval()  )
```
    eval(df_formular_text)
    
``` 
