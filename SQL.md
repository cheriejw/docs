### (T-)SQL:  [Base List](https://www.techonthenet.com/sql/index.php)
---
#### Not included:
- [DATE functions](https://www.tutorialspoint.com/t_sql/t_sql_date_functions.htm)
- Set Statistics Time
```sql
SET STATISTICS TIME ON;
GO
declare @p9 varchar(1000)
set @p9=''
exec ECAdmin.ecsp_DoActionRemitCategory @LogInUserId=1834,@InstitutionId=8163,@FromIpAddress=N'::1',@FromDomain=N'::1',@RemitCategoryDescr=N'dup2',@RemitCategoryCd=N'dup2',@IsValid='Y',@Action='add',@ErrMsg=@p9 output
select @p9
GO
SET STATISTICS TIME OFF;
GO
-- I have just been taking time before the Row Affected line:
-- SQL Server Execution Times:
-- CPU time = 16 ms,  elapsed time = 4 ms. 
```
- [Pivot](https://technet.microsoft.com/en-us/library/ms177410(v=sql.105).aspx) - PIVOT executes like UNION
```sql
select * from RemitFormFieldAssoc rffa
select * from RemitFormFieldAssoc rffa pivot (max(RemitFormId) for RemitFieldColNum in ([0],[1],[2],[3],[4],[5])) as maxId
    -- new select missing remitformid column and remitfieldcolnum column. Added 1-5 column at top with formid in the row under the cols.
```

- [@@IDENTITY](https://docs.microsoft.com/en-us/sql/t-sql/functions/identity-transact-sql): Will give you the last identifier of what you accessed. Does not include deletes.
```sql
insert into RemitLog (RemitFormId,RemitFormValueXml,IsValid)
values (30,'<test></test>','Y')
select @@IDENTITY as 'Id'
```

- [Using SET or using SELECT](https://www.mssqltips.com/sqlservertip/1888/when-to-use-set-vs-select-when-assigning-values-to-variables-in-sql-server/)
```sql
SET @Var2ForSet = (SELECT [Name] FROM Production.Product WHERE Color = 'Silver')
-- or
SELECT @Var2ForSelect = [Name] FROM Production.Product WHERE Color = 'Silver'
```
>Whenever you are assigning a query returned value to a variable, SET will accept and assign a scalar (single) value from a query. While SELECT could accept multiple returned values. But after accepting multiple values through a SELECT command you have no way to track which value is present in the variable. The last value returned in the list will populate the variable. Because of this situation it may lead to un-expected results as there would be no error or warning generated if multiple values were returned when using SELECT. So, if multiple values could be expected use the SET option with proper implementation of error handling mechanisms.

- [ANY/ALL Operator](https://www.w3schools.com/sql/sql_any_all.asp)
```sql
SELECT 1 
FROM dbo.RemitCategory rc WITH(NOLOCK)
WHERE @InstitutionTypeId = @NETWORKINSTITUTIONTYPE -- Check only if it is a Network
	AND (rc.RemitCategoryCd = @RemitCategoryCd OR rc.RemitCategoryDescr = @RemitCategoryDescr)
	AND rc.InstitutionId = ANY(SELECT i.InstitutionId FROM Institution i WHERE i.NetworkId = @NetworkId)
	-- Get all institution in network if network.
```
- [OVER Clause](https://msdn.microsoft.com/en-us/LIBRARY/ms189461(v=sql.105).aspx)

```sql
WITH t AS ( -- cte
  SELECT InfoDate d,ROW_NUMBER() OVER(ORDER BY InfoDate) i
  FROM @d
  GROUP BY InfoDate
)
SELECT MIN(d),MAX(d)
FROM t
GROUP BY DATEDIFF(day,i,d)
```

- [CTE](https://stackoverflow.com/questions/11169550/is-there-a-performance-difference-between-cte-sub-query-temporary-table-or-ta)
```SQL
;WITH cte AS (
	SELECT DISTINCT
		aep.AlertMethodId,
		am.AlertMethodDescr
	FROM
		dbo.AlertEventPolicy aep WITH(NOLOCK) 
		INNER JOIN AlertMethod am WITH(NOLOCK) ON am.AlertMethodId = aep.AlertMethodId
	WHERE
		aep.InstitutionId = @AcquirerId 
		AND aep.AlertEventId IN (@MULTICHECKRECEIPT, @SINGLECHECKRECEIPT, @PURCHASERECEIPT)
		AND aep.IsValid = 'Y'
		AND am.IsValid = 'Y'
)
SELECT
	rdpam.RemoteDepositPolicyAlertMethodId,
	rdpam.RemoteDepositPolicyId,
	rdp.RemoteDepositPolicyDescr,
	cte.AlertMethodId,
    cte.AlertMethodDescr,
	rdpam.IsRegisteredAddressUsed,
	rdpam.IsExtraAddressAllowed,
	rdpam.IsValid,
	rdpam.RowVer   
FROM
	RemoteDepositPolicyAlertMethod  rdpam WITH(NOLOCK)
	INNER JOIN @RemoteDepositPolicy rdp ON rdp.RemoteDepositPolicyId = rdpam.RemoteDepositPolicyId
	CROSS APPLY	cte
WHERE
	rdpam.IsValid = 'Y'
```

---

### Unit Tests
_Arrange, Act, Assert_
[Unit Test Naming Conventions](https://dzone.com/articles/7-popular-unit-test-naming)


#### Unit Tests (tsqlt)
_Arrange, Act, Assert_
[Unit Test Naming Conventions](https://dzone.com/articles/7-popular-unit-test-naming)
SQL Server Execution Times:
   CPU time = 16 ms,  elapsed time = 4 ms. 