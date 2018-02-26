## SQL
---
#### [Using SET or using SELECT](https://www.mssqltips.com/sqlservertip/1888/when-to-use-set-vs-select-when-assigning-values-to-variables-in-sql-server/)
```sql
SET @Var2ForSet = (SELECT [Name] FROM Production.Product WHERE Color = 'Silver')
-- or
SELECT @Var2ForSelect = [Name] FROM Production.Product WHERE Color = 'Silver'
```
>Whenever you are assigning a query returned value to a variable, SET will accept and assign a scalar (single) value from a query. While SELECT could accept multiple returned values. But after accepting multiple values through a SELECT command you have no way to track which value is present in the variable. The last value returned in the list will populate the variable. Because of this situation it may lead to un-expected results as there would be no error or warning generated if multiple values were returned when using SELECT. So, if multiple values could be expected use the SET option with proper implementation of error handling mechanisms.