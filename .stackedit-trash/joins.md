# Descartes-szorzat
`R CROSS JOIN S`
# Belső
## Természetes
`R NATURAL JOIN S`
## Théta
`R JOIN S ON <feltétel>`
## Félig
```sql
SELECT column1
FROM table1
WHERE EXISTS(SELECT column2 FROM table2 WHERE ...)
```
## Anti
```sql
SELECT column1
FROM table1
WHERE NOT EXISTS(SELECT column2 FROM table2 WHERE...)
```
# Külső
Kiterjesztett relációs algebra
$R$ azon sorait, melyeknek nincs $S$-beli párja **lógó** soroknak nevezzük ($S$-nek is lehetnek lógó sorai)
A külső összekapcsolás megőrzi a lógó sorokat `NULL` értékkel helyettesítve a hiányzó értékeket
# Left

# Right

# Outer
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2ODU3ODc5NV19
-->