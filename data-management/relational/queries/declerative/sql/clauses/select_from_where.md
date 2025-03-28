# SELECT
`SELECT` az érdekes attribútumok

```sql
SELECT column1 FROM

-- * a záradékban a reláció összes attribútuma
SELECT * FROM
```
## Attribútumok átnevezése
```sql
SELECT column1 as column2 FROM
```
## Értékek felüldefiniálása
```sql
SELECT number*15 as new_number FROM
```
## Konstans
```sql
SELECT "World" as Hello
```
## DISTINCT
Törli a kapott lekérdezésben szereplő duplikátumokat
```sql
SELECT DISTINCT column1 FROM
```
# FROM
`FROM` egy vagy több tábla

Képzeletbeli sorváltozók, ha a sorváltozók a `WHERE` záradékot kielégítő feltételre mutatnak a sor a `SELECT` záradéknak továbbítódik
```sql
FROM table

FROM table as table_name

FROM table as t1, table as t2
```
## Alkérdések
Zárójelezett `SELECT-FROM-WHERE` utasításokat (alkérdéseket) is használhatunk

**Egy sort visszaadó alkérdés** úgy használható, mint egy konstans érték, általában egy erdemény sornak egyetlen oszlopa van
```sql
FROM (SELECT ... FROM ... WHERE)
```
# WHERE
* `WHERE` a táblák soraira vonatkozó feltételek
## Alkérdés*
```sql
WHERE (SELECT column FROM ... WHERE)
```
## Három-értékű logika
* `TRUE`
* `FALSE`
* `UNKNOWN`

Ha egy értéket `NULL`-lal hasonlítunk `UNKNOWN`-ot kapunk

Egy sor akkor és csak akkor kerül be az eredménybe, ha a `WHERE` záradék `TRUE` értéket ad
## Összetett feltételek `WHERE` záradékban
### Logikai
* `AND`
* `OR`
* `NOT`
### Összehasonlítás
* `=`
* `<>`
* `<`
* `>`
* `<=`
* `>=`
### LIKE
A feltételekben a sztringeket mintákra illeszthetjük
```sql
<attribute> LIKE <pattern>

<attribute> NOT LIKE <pattern>
```

* `%` nulla vagy több karakter
* `_` pontosan egy karakter
* `^` minden nem ilyen karakter
* `-` minden karakter az adott tartományban 
```sql
LIKE `Hungar_`
LIKE `[abc]%` -- a, b vagy c-vel kezdődik
LIKE `[a-c]%`
LIKE `[!def]%` -- nem kezdődik d, e vagy f-el
NOT LIKE `[def]%`
```
### IN
`<sor> IN (<subquery>)` igaz akkor és csak akkor, ha a sor eleme az alkérdés eredményének
`<sor> NOT IN (<subquery>)`
```sql
WHERE column IN (value1, value2, ...) --value in a set of value

IN (SELECT STATEMENT)
```
### EXISTS
 `EXISTS (<subquery>)` akkor és csak akkor igaz, ha az alkérdés eredménye nem üres
### ANY
`column <operator> ANY (<subquery>)` akkor és csak akkor igaz, ha `x` megfelel az operátor által definiált, az alkérdés bármely elemének
### ALL
`column <operator> ALL(<subquery>)` akkor és csak akkor igaz, ha `x` megfelel az operátor által definiált, az alkérdés összes elemének
#### Halmaz műveletek
```sql
(<subquery>) UNION (<subquery>)

(<subquery>) INTERSECT (<subquery>)

(<subquery>) EXCEPT (<subquery>)
```
`SELECT-FROM-WHERE` állítások **multihalmaz szemantikát** használnak, azaz lekérdezések eredményeiben azonos értékek többször is előfordulhatnak, ha a bemeneti halmazokban azok többször is előfordulnak

A halmazműveleteknél mégis a **halmaz szemantika** az érvényes, miszerint a sorok nem ismétlődnek kiválasztáskor
Az `ALL` záradékkal definiálva a műveletet multihalmaz szemantikát kapunk
```sql
(<subquery>) UNION ALL (<subquery>)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNjE5NzIyOThdfQ==
-->