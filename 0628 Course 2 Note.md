# 0628 Course 2 Note

View the Notes with HackMD.

SSMS 設定定序
---

- _BIN 指定使用向後兼容的二進制排序順序
- _BIN2 指定使用SQL SERVER 2005 中引入的碼位比較語意的二進制排序順序
- _Stroke 按筆畫排序
- _CI(CS) 是否區分大小寫，CI不區分，CS區分
- _AI(AS) 是否區分重音，AI不區分，AS區分
- _KI(KS) 是否區分假名類型，KI不區分，KS區分
- _WI(WS) 是否區分全半角，WI不區分，WS區分

SQL 指定 COLLATE
---

SELECT * FROM Person.Address
WHERE AddressLine1 COLLATE Chinese_Taiwan_Bopomofo_90_CS_AI
LIKE '1970napa%'

重建系統資料庫
---

- 預設的Path
C:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012

- 注意路徑上的版本號，因為有可能Server上會有多個版本

登入SQL Server
---

- 登入選項可以挑選使用者登入系統後的顏色(提醒自己在哪一台機器)

Data Manipulation Language (DML)
---

- SELECT, INSERT, UPDATE, DELETE

Data Definition Language (DDL)
---

- CREATE, ALTER, DROP

Data Control Language (DCL)
---

- GRANT, REVOKE, DENY

T-SQL Language Elements
---

- Predicates and Operators
IN, BETWEEN, LIKE
=, >, <, >=, <=, <>, !=, !>, !<
AND, OR, NOT
+, -, *, /, %
- Function
- Variables
Declare @qty int
- Control of Flow, Errors and Transactions
IF...ELSE..., WHILE, TRY...CATCH..., Begin Transaction,
Commit, Rollback
- Comments
/* ... */ & - 

SELECT 查詢順序
---

- 5:SELECT
- 1:FROM
- 2:WHERE
- 3:GROUP BY
- 4:HAVING
- 6:ORDER BY

TOP
---
	
SELECT TOP (num) 

- Group By 重複仍會顯示出來
SELECT TOP (num) WITH TIES 
GROUP BY 

取DATETIME
---

- YEAR(Datetime)
- MONTH(Datetime)
- DAY(Datetime)

CASE WHEN 語法
---
- CASE WHEN (Variable) IN (Condition) THEN (Do Something) END

建立類似View表
---
- WITH (Name) AS ( SELECT 語句 )
	
GROUP 列 轉 欄
---
- SUM(CASE (變數) WHEN (條件) THEN (結果) ELSE (例外結果) END)

PIVOT 列 轉 欄 (數字分組加總)
---
- COALESCE((Condition), (例外則))
- PIVOT(SUM(Cnt) FOR (View表SELECT之值) IN (CONDITION) )

SELECT ClassId,
       ClassName,
       COALESCE([2016], 0) AS CNT2016,
	   COALESCE([2017], 0) AS CNT2017,
	   COALESCE([2018], 0) AS CNT2018,
	   COALESCE([2019], 0) AS CNT2019
FROM YearNumber
PIVOT(
    SUM(Cnt)
    FOR Year IN ([2016], [2017], [2018], [2019])
) AS PV
ORDER BY ClassId

合併欄位
---
- CONCAT((Column1),(Column2),(Column3).....)

CROSS APPLY JOIN
---
- CROSS APPLY(SELECT ..... FROM ...... WHERE (關聯))

交易
---
- TRY 裡面 包TRANSACTION
- INSERT
BEGIN TRY
	BEGIN TRANSACTION;
		INSERT INTO BOOK_LEND_RECORD(KEEPER_ID, BOOK_ID, LEND_DATE)
		VALUES ('0002', 2004, GETDATE());
	COMMIT TRANSACTION;
END TRY

BEGIN CATCH
      ROLLBACK TRAN;
      THROW;
END CATCH

- UPDATE
BEGIN TRY
	BEGIN TRANSACTION;
		UPDATE BOOK_LEND_RECORD
        SET LEND_DATE = CAST('2019-01-02' AS DATETIME)
        WHERE KEEPER_ID = 0002
	COMMIT TRANSACTION;
END TRY

BEGIN CATCH
      ROLLBACK TRAN;
      THROW;
END CATCH

- DELETE
BEGIN TRY
	BEGIN TRANSACTION;
		DELETE FROM dbo.BOOK_LEND_RECORD
        WHERE BOOK_ID = 2004
	COMMIT TRANSACTION;
END TRY

BEGIN CATCH
      ROLLBACK TRAN;
      THROW;
END CATCH




Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `SQL`
