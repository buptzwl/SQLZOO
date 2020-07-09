# 	SQLZOO刷题
## SELECT basics
>1.字串應該在'單引號'中。  
**修改此例子,以顯示德國 Germany 的人口**

```sql 
SELECT population FROM world WHERE name = 'Germany '
```

>2.可用公式計算。  
**修改此例子,查詢面積為 5,000,000 以上平方公里的國家,對每個國家顯示她的名字和人均國內生產總值(gdp/population)。**

```sql
 SELECT name, gdp/population FROM world WHERE area > 5000000
```

>3.檢查列表:單詞“IN”可以讓我們檢查一個項目是否在列表中。  
**顯示“Ireland 愛爾蘭”,“Iceland 冰島”,“Denmark 丹麥”的國家名稱和人口**

```sql
 SELECT name, population FROM world WHERE name IN ('Ireland ', 'Iceland ', 'Denmark ')
```

>4.BETWEEN 允許範圍檢查 - 注意,這是包含性的。  
**修改此例子,以顯示面積為 200,000 及 250,000 之間的國家名稱和該國面積。**

```sql
SELECT name, area FROM world WHERE area BETWEEN 200000 AND 250000
```

## SELECT names
>1.你可以用WHERE name LIKE 'B%'來找出以 B 為開首的國家。
%是萬用字元,可以用代表任何字完。  
**找出以 Y 為開首的國家**
```sql
SELECT name FROM world WHERE name LIKE 'Y%'
```
>2.**找出以 Y 為結尾的國家**
```sql
SELECT name FROM world WHERE name LIKE '%Y'
```
>3.**找出所有國家,其名字包括字母x**
```sql
SELECT name FROM world WHERE name LIKE '%x%'
```

>4.**找出所有國家,其名字以 land 作結尾**
```sql
SELECT name FROM world WHERE name LIKE '%land'
```

>5.**找出所有國家,其名字以 C 作開始,ia 作結尾**
```sql
SELECT name FROM world WHERE name LIKE 'C%ia'
```

>6.**找出所有國家,其名字包括字母oo**
```sql
SELECT name FROM world WHERE name LIKE '%oo%'
```

>7.**找出所有國家,其名字包括三個或以上的a**
```sql
SELECT name FROM world WHERE name LIKE '%a%a%a%'
```

>8.你可以用底線符_當作單一個字母的萬用字元  
**找出所有國家,其名字以t作第二個字母**
```sql
SELECT name FROM world WHERE name LIKE '_t%' ORDER BY name
```

>9.**找出所有國家,其名字都有兩個字母 o,被另外兩個字母相隔着**
```sql
SELECT name FROM world WHERE name LIKE '%o__o%'
```

>10.length()函数的使用  
**找出所有國家,其名字都是 4 個字母的**
```sql
SELECT name FROM world WHERE length(name) = 4 
```

>11.**顯示所有國家名字,其首都和國家名字是相同的**
```sql
SELECT name FROM world WHERE name = capital
```


>12.concat函数的使用
**顯示所有國家名字,其首都是國家名字加上” City”**
```sql
SELECT name FROM world WHERE capital = concat(name,' City')
```
>13.**找出所有首都和其國家名字,而首都要有國家名字中出現**
```sql
SELECT capital,name FROM world WHERE capital like concat('%',name,'%')
```

>14.**找出所有首都和其國家名字,而首都是國家名字的延伸**
```sql
SELECT name,capital FROM world WHERE capital like concat(name,'_%')
```

>15.replace()函数的使用  
**顯示國家名字，及其延伸詞，如首都是國家名字的延伸**
```sql
SELECT `name`, replace(capital,`name`,'') affix FROM world WHERE capital like concat(`name`,'_%')
```

## SELECT from world
>1.介绍

>2.**顯示具有至少2億人口的國家名稱。**
```sql
SELECT name FROM world WHERE population>200000000
```

>3.**找出有至少200百萬(2億)人口的國家名稱，及人均國內生產總值。**
```sql
SELECT name,gdp/population FROM world WHERE population>200000000
```

>4.**顯示'South America'南美洲大陸的國家名字和以百萬為單位人口數。**
```sql
SELECT name,population/1000000 FROM world WHERE continent = 'South America'
```


>5.**顯示法國，德國，意大利(France, Germany, Italy)的國家名稱和人口。**
```sql
SELECT name,population FROM world WHERE name in ('France','Germany','Italy')
```

>6.**顯示包含單詞“United”為名稱的國家。**
```sql
SELECT name FROM world WHERE name like '%United%'
```

>7.成為大國的兩種方式：如果它有3百萬平方公里以上的面積，或擁有250百萬(2.5億)以上人口。  
**展示大國的名稱，人口和面積**
```sql
SELECT name,population,area FROM world WHERE population>250000000 or area>3000000
```

>8.使用异或XOR  
**顯示以人口或面積為大國的國家，但不能同時兩者。顯示國家名稱，人口和面積。**
```sql
SELECT name,population,area FROM world WHERE population>250000000 xor area>3000000
```

>9.使用ROUND函数
>
>**對於南美顯示以百萬計人口，以十億計2位小數GDP**
>
>round(population/100000000,n),n代表的是小数点后n位
```sql
select name,round(population/1000000,2),round(gdp/1000000000,2) from world 
where continent ='South America'
```

>10.**顯示萬億元國家的人均國內生產總值，四捨五入到最近的$ 1000**。
```sql
select name,round(gdp/population,-3) from world where gdp>1000000000000
```

>11.**Show the name - but substitute** **Australasia** **for** **Oceania** **- for countries beginning with N.**
```sql
SELECT name,
       CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
 FROM world
 WHERE name LIKE 'N%'
```

## SELECT from Nobel 

>1.**更改查詢以顯示1950年諾貝爾獎的獎項資料。**

```sql
SELECT yr, subject, winner FROM nobel WHERE yr =1950
```

>2.**顯示誰贏得了1962年文學獎(Literature)。**

```sql
SELECT winner FROM nobel WHERE yr = 1962 AND subject = 'Literature'
```

>3.**顯示“愛因斯坦”('Albert Einstein') 的獲獎年份和獎項。**

```sql
SELECT yr,subject FROM nobel WHERE winner='Albert Einstein'
```

>4.**顯示2000年及以後的和平獎(‘Peace’)得獎者。**

```sql
SELECT winner FROM nobel WHERE subject='Peace' and yr>=2000
```
>4.**顯示2000年及以後的和平獎(‘Peace’)得獎者。**

```sql
SELECT winner FROM nobel WHERE subject='Peace' and yr>=2000
```

>5.**顯示1980年至1989年(包含首尾)的文學獎(Literature)獲獎者所有細節（年，主題，獲獎者）。**

```sql
SELECT yr,subject,winner FROM nobel 
WHERE subject='Literature'and yr between 1980 and 1989
```

>6.**顯示總統獲勝者的所有細節。**

```sql
SELECT * FROM nobel
WHERE  winner IN ('Theodore Roosevelt','Woodrow Wilson','Jimmy Carter')
```

>7.**顯示名字為John 的得獎者。 (注意:外國人名字(First name)在前，姓氏(Last name)在後)。**

```sql
SELECT winner FROM nobel where winner like 'John%'
```

>8.**顯示1980年物理學(physics)獲獎者，及1984年化學獎(chemistry)獲得者。**

```sql
SELECT yr,subject,winner FROM nobel 
WHERE 
(subject='physics' and yr = 1980) or (subject='chemistry' and yr = 1984)
```

>9.**查看1980年獲獎者，但不包括化學獎(Chemistry)和醫學獎(Medicine)。**

```sql
SELECT yr,subject,winner FROM nobel 
WHERE yr = 1980 and subject not in('Chemistry','Medicine')
```

>10.**顯示早期的醫學獎(Medicine)得獎者（1910之前，不包括1910），及近年文學獎(Literature)得獎者（2004年以後，包括2004年）。**

```sql
SELECT yr,subject,winner FROM nobel 
WHERE 
(subject='Medicine' and yr <1910) or (subject='Literature' and yr>=2004)
```

>11.**Find all details of the prize won by PETER GRÜNBERG。**

```sql
SELECT yr,subject,winner FROM nobel WHERE winner='PETER GRÜNBERG'
```
