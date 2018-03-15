## SQL
---
#### [CTE](https://stackoverflow.com/questions/11169550/is-there-a-performance-difference-between-cte-sub-query-temporary-table-or-ta)
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

#### [AlterAuthorization (SID)](https://stackoverflow.com/questions/12389656/the-database-owner-sid-recorded-in-the-master-database-differs-from-the-database)
Reset owner of DB.
```SQL
DECLARE @user VARCHAR(50)
SELECT @user = quotename(SL.Name)
FROM master..sysdatabases SD 
    INNER JOIN master..syslogins SL ON SD.SID = SL.SID
WHERE SD.Name = DB_NAME()
EXEC('EXEC sp_changedbowner ' + @user)
```

#### [Using SET or using SELECT](https://www.mssqltips.com/sqlservertip/1888/when-to-use-set-vs-select-when-assigning-values-to-variables-in-sql-server/)
```sql
SET @Var2ForSet = (SELECT [Name] FROM Production.Product WHERE Color = 'Silver')
-- or
SELECT @Var2ForSelect = [Name] FROM Production.Product WHERE Color = 'Silver'
```
>Whenever you are assigning a query returned value to a variable, SET will accept and assign a scalar (single) value from a query. While SELECT could accept multiple returned values. But after accepting multiple values through a SELECT command you have no way to track which value is present in the variable. The last value returned in the list will populate the variable. Because of this situation it may lead to un-expected results as there would be no error or warning generated if multiple values were returned when using SELECT. So, if multiple values could be expected use the SET option with proper implementation of error handling mechanisms.