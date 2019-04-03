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

### Function

avg() : 取平均
max() : 取最大值
min() :取最小值
sum() : 計算總和
count(*) : 計算table中有幾筆資料
round(num,length) : 四捨五入


### Like

功能 :字串比對

% : 代表零個或一個以上的任意字元
_ : 代表單一個數的任意字元 


    where Name like "A%“

    where Name like "A_“

    where Name like “A_ _“

    where Name like "%e“

    where Name like "%c%"


### Between / And範圍條件

功能 : 用來指定一個範圍，資料值必須在最小值與最大值之間(含最大值、最小值)

select * from my_database.class
   where Age between 13 and 15
   //Age要在13~15之間(含13、15)
   
### Case…When….Then

    select *,
      case
        when Height < 60 then "short"
        when Height < 70 then "normal"
        else "tall"
      end as result
       from my_database.class

### IN集合條件

功能 : 只要有出現在集合中的元素都會被選取

select * from my_database.class
   where Age IN(12,15)

select * from my_database.class
   where Age NOT IN(12,15)	//留下沒出現在集合中的元素

### IS NULL / IS NOT NULL

NULL表示欄位中沒有任何的值
IS NULL : 若該欄位是NULL就回傳True，否則False
IS NOT NULL : 若該欄位不是NULL就回傳True，否則False

select * from my_database.class
   where Age is NULL

Group By

功能 : 依照某些欄位的值進行分組，有相同的值就分在一組

select Age , avg(Weight) from my_database.class
   group by Age
   
Having

功能 : 對GROUP BY分組後的結果再次過濾

select * from my_database.car
	group by Make
	Having count(Make) < 8

where 先過濾資料，再進行運算
Having 先進行運算，再過濾資料

### Order By

功能 : 對資料進行排序

select * from my_database.class
   order by Height asc	//由小到大排序(可以省略)

select * from my_database.class
   order by Height desc	//由大到小排序(不可省略)

(若無指定則默認為asc)

### Inner Join

功能 : 取交集

select Name,Score from class inner join score
   	   on class.Name == score.Name
       
### Left Outer Join
功能 :包含left table的所有資料

select Name as left_table from score left outer join class
	on score.Name == class.Name

### Right Outer Join
功能 : 包含right table的所有資料

SQLite不支持Right Outer Join和Full Outer Join。
將Left join的左右table互換即可實現Right Outer Join的效果。
  select Name as left_table from class left outer join score
    on score.Name == class.Name


### Full Outer Join 

功能 : 結合了left join 和 right join 的結果------>聯集

  select append1.* from append1 left outer join append2
    on append1.ID == append2.ID
    union
    select append2.* from append2 left outer join append1
    on append2.ID == append1.ID


### Cartesian Product

功能 : 兩個table在join時，不指定任何條件，即將兩個table中所有的可能排列組合出來。

If the left table has 5 rows and the right table has 6 rows, 30 rows of output will be produced.

select Name,Score from class cross join score


### 子查詢(Subquery)

子查詢是一個放在左右刮號中的「SELECT」敘述，而這個查詢敘述會放在另一個SQL敘述中。

子查詢大部份使用在提供判斷條件用的資料，在「WHERE」和「HAVING」子句中，都可能出現子查詢。

select Name,Sex,Age from student_data
   	where Name in
		(select Name from your_student);
    
    

### 集合運算子

集合運算時，上下table的column數量、名稱、順序必須一樣。

種類 : 
	1、Union
	2、Intersection
	3、Difference


### Union

功能 : 聯集，將上下表合併起來，且會去除重複的資料列。

select *
	from append1
  	    union
   select *
	from append2
   order by ID

Union ALL 不會去掉重複的資料列。
垂直合併，二個table的欄位數量、名稱、順序必須一樣。


### Intersection

功能 : 交集。

select *
	from append1
  	    intersect
   select *
	from append2
   order by ID



### Difference

功能 : 差集，將表一的資料減去表二的資料所得的結果。

select *
	from append1
  	    except
   select *
	from append2
   order by ID

會刪除重複的資料列





