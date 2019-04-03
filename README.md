# SQLite-Tutorial


### Select語句

  功能 :擷取table中一個或多個column的資料

  基本語法
  
   SELECT column1, column2, columnN FROM table_name;

    - 擷取所有column的資料
      select * from my_database.class

    - 擷取指定column的資料
      select Name from my_database.class

### As語句

功能:可以使用不同的名稱來顯示原本的column名稱

(As只是暫時性的變更column名稱，並不會真的把原本的column名稱覆蓋過去)

  基本語法

  SELECT column_name AS alias_name
  FROM table_name

    - select Name as New_Name from my_database.class

    - select Name as [New Name] from my_database.class
       -使用[新名稱]可以顯示空格或特殊字元

### 字串連接

select Name ||"-"|| Age from my_database.class
   - 以”-”這個符號來連接Name和Age這二個column的資料

select Name ||"-"|| Age as [Name-Age] 
   from my_database.class

### Distinct關鍵字

功能 : 消除重複的資料列

  基本語法

  SELECT DISTINCT column1, column2,.....columnN 
  FROM table_name

    select distinct Sex from my_database.class

    select distinct Sex,Age from my_database.class
       -如果select distinct包含多個column，則依照所有column的組合來決
         定資料列的唯一性
         
### 算術運算子

+
-
*
/
% : 取餘數


### 比較運算子

== (等於)
<> (不等於)
< (小於)
<= (小於等於)
> (大於)
>= (大於等於)

### 邏輯運算子

And : 所有條件都要成立才會回傳true
Or : 只要有一個條件成立就回傳true
Not : 反轉，可以把true變成false，false變成true


### Where字句

功能 : 篩選資料

  基本語法

  SELECT column1, column2, columnN 
  FROM table_name
  WHERE [condition]


    select * from my_database.class
       where Age > 13

