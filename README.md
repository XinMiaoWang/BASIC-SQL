# SQLite-Tutorial


### 一、SQLite Studio 安装

   &emsp;[在 Windows 上安裝 SQLite Studio](https://sqlitestudio.pl/index.rvt)

### 二、SQL基本語法

![](https://i.imgur.com/k4WyjLK.png)


### Select語句

  * 功能 : 擷取table中一個或多個column的資料

  * 基本語法
  
  	***SELECT column1, column2, columnN FROM table_name;***

	    - 擷取所有column的資料('*'代表所有的column)
	      select * from mydb.class
	      
	![](https://i.imgur.com/8YuUfVL.png)
		
	    - 擷取指定column的資料
	      select Name from mydb.class
	      
	![](https://i.imgur.com/QsXPgTm.png)

### As語句

  * 功能:可以使用不同的名稱來顯示原本的column名稱

    (As只是暫時性的變更column名稱，並不會真的把原本的column名稱覆蓋過去)

  * 基本語法

  	***SELECT column_name AS alias_name FROM table_name***

    	select Name as New_Name from mydb.class
	
	  ![](https://i.imgur.com/mUjyRhI.png)
	
    	select Name as [New Name] from mydb.class
       	使用[ ]可以顯示空格或特殊字元
	  
	  ![](https://i.imgur.com/qUrUTAB.png)

### 字串連接

   	- 以"-"這個符號來連接Name和Age這二個column的資料
   	  select Name ||"-"|| Age from mydb.class

   ![](https://i.imgur.com/HnHnQOQ.png)

	- 產生的column name 不太好看，我們可以用as來為他取個新名稱
	  select Name ||"-"|| Age as [Name-Age] from mydb.class
	  
   ![](https://i.imgur.com/tVC57Bh.png)

### Distinct關鍵字

  * 功能 : 消除重複的資料列

  * 基本語法

  	***SELECT DISTINCT column1, column2,.....columnN FROM table_name***

    	select distinct Sex from mydb.class
	
	![](https://i.imgur.com/ntbIw6S.png)

    	select distinct Sex,Age from mydb.class
       	-如果select distinct包含多個column，則依照所有column的組合來決定資料列的唯一性
	
	![](https://i.imgur.com/9xboW2w.png)
         
	 
### 算術運算子

	+ : 加法
	- : 減法
	* : 乘法
	/ : 除法
	% : 取餘數 ex. 8 % 5 = 3


### 比較運算子

	== (等於)
	<> (不等於)
	< (小於)
	<= (小於等於)
	> (大於)
	>= (大於等於)

### 邏輯運算子

	And : 所有條件都要成立才會回傳true。
	Or : 只要有一個條件成立就回傳true。
	Not : 反轉，可以把true變成false，false變成true。


### Where字句

  * 功能 : 篩選資料

  * 基本語法

  	***SELECT column1, column2, columnN FROM table_name***
  
  	&emsp;***WHERE [condition]***

	    select * from mydb.class
	       where Age > 13
	       
	    (where後面放條件)
	    
    ![](https://i.imgur.com/z4p6GcS.png)

### 常用Function

	  avg() : 取平均
	  max() : 取最大值
	  min() :取最小值
	  sum() : 計算總和
	  count(*) : 計算table中有幾筆資料
	  round(num,length) : 四捨五入


### Like

* 功能 : 字串比對

	% : 代表零個或一個以上的任意字元

	_ : 代表單一個任意字元 


	    where Name like "A%"

	    where Name like "A_"

	    where Name like “A_ _"

	    where Name like "%e"

	    where Name like "%c%"


### Between / And 範圍條件

 * 功能 : 用來指定一個範圍，資料值必須在最小值與最大值之間(含最大值、最小值)

		select * from mydb.class
		   where Age between 13 and 15
		   
   會篩選出Age在13~15之間的資料   
   
   ![](https://i.imgur.com/ogmbhkY.png)

   
### Case…When…Then

    select *,
      case
        when Height < 60 then "short"
        when Height < 70 then "normal"
        else "tall"
      end as result
       from mydb.class
       
   ![](https://i.imgur.com/e9e9rvk.png)


### IN集合條件

  * 功能 : 只要有出現在集合中的元素都會被選取

		select * from mydb.class
		   where Age IN(12,15)
		
	![](https://i.imgur.com/iWh1zl4.png)
	
		- 留下沒出現在集合中的元素
			select * from mydb.class
			where Age NOT IN(12,15)
			
       ![](https://i.imgur.com/nZclU8o.png)

### IS NULL / IS NOT NULL

	NULL表示欄位中沒有任何的值
	IS NULL : 若該欄位是NULL就回傳True，否則False
	IS NOT NULL : 若該欄位不是NULL就回傳True，否則False


	select * from mydb.class
	   where Age is NULL


### Group By

  * 功能 : 依照某些欄位的值進行分組，有相同的值就分在一組

		select Age , avg(Weight) from mydb.class
		   group by Age
		   
   ![](https://i.imgur.com/wmhBKh4.png)


### Having

  * 功能 : 對GROUP BY分組後的結果再次過濾

		select * from mydb.class
			group by Age
			Having avg(Weight) > 100
			
	![](https://i.imgur.com/4hRLdWw.png)


	***where 先過濾資料，再進行運算***

	***Having 先進行運算，再過濾資料***


### Order By

  * 功能 : 對資料進行排序
		
		- 由小到大排序(可以省略asc)
		  select * from mydb.class
		     order by Height asc
		
	![](https://i.imgur.com/n0pxkgt.png)
		
		- 由大到小排序(不可省略desc)
		  select * from mydb.class
		     order by Height desc
		     
	![](https://i.imgur.com/jaWqUf5.png)
	
	***若無指定則默認為asc***



### 三、合併(Join)

![](https://i.imgur.com/FWWIBDO.png)


### Inner Join

  * 功能 : 取交集
  
	![](https://i.imgur.com/wZh0e3t.png)

		select Name,Score from class inner join score
			   on class.Name == score.Name
       
### Left Outer Join

  * 功能 :包含left table的所有資料

		select Name as left_table from score left outer join class
			on score.Name == class.Name

### Right Outer Join

  * 功能 : 包含right table的所有資料
  
	***SQLite不支持Right Outer Join和Full Outer Join。***
	
	***將Left join的左右table互換即可實現Right Outer Join的效果***
	
		  select Name as left_table from class left outer join score
		    on score.Name == class.Name


### Full Outer Join 

  * 功能 : 結合了left join 和 right join 的結果------>聯集

		  select append1.* from append1 left outer join append2
		    on append1.ID == append2.ID
		    
		    union
		    
		  select append2.* from append2 left outer join append1
		    on append2.ID == append1.ID


### Cartesian Product

  * 功能 : 兩個table在join時，不指定任何條件，即將兩個table中所有的可能排列組合出來。

	ex. If the left table has 5 rows and the right table has 6 rows, 30 rows of output will be produced.

		select Name,Score from class cross join score

### 四、子查詢(Subquery)


### 子查詢(Subquery)

  * 子查詢是一個放在左右刮號中的「SELECT」敘述，而這個查詢敘述會放在另一個SQL敘述中。

  * 子查詢大部份使用在提供判斷條件用的資料，在「WHERE」和「HAVING」子句中，都可能出現子查詢。

		select Name,Sex,Age from student_data
		  where Name in
		    (select Name from your_student);
    
    
### 五、集合運算子


### 集合運算子

  * 種類 : 
  
	1、Union
	
	2、Intersection
	
	3、Difference
	
  ***集合運算時，上下table的column數量、名稱、型態、順序必須一樣***


### Union

  * 功能 : 聯集，將上下表合併起來，且會去除重複的資料列。

		select *
			from Appending01
			
		union
		
		select *
			from Appending02
		   order by ID

  	***Union ALL 不會去掉重複的資料列***


### Intersection

  * 功能 : 交集。

		select *
			from Appending01
			
		intersect
		
		select *
			from Appending02
		   order by ID



### Difference

  * 功能 : 差集，將表一的資料減去表二的資料所得的結果。

		select *
			from Appending01
			
		except
		
		select *
			from Appending02
		   order by ID

	***會刪除重複的資料列****





