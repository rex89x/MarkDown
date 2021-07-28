# Oracle PL/SQL Code Note

Dynamic Query Code
---

```sql
// 模糊查詢
SELECT * FROM database WHERE column1 LIKE CONCAT(CONCAT('%', '@param'), '%')
```

```sql
-- 動態查詢 VB.NET 語法
SELECT COUNT(DISTINCT SEQ_NO) AS SEQ_NO FROM LMBM_CHK_CASE " _
                & " WHERE SEQ_NO =\?S 
```








Rex Tsou 2021/06/28

###### tags: `Work` `Sample` `Dot Net`