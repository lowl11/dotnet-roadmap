# Транзакции / Transaction

**Транзакция** - это набор запросов в БД объединенных в одну пачку.
```SQL
BEGIN TRANSACTION
<some sql actions>
COMMIT / ROLLBACK
END
```