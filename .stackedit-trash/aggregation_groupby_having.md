# Aggregációk
Összesítő függvényeket a `SELECT` záradékban alkalmazhatjuk egy-egy oszlopra

`NULL` értékek nem számítanak az összesítésben, ha csak `NULL` van, akkor az eredmény is `NULL`
* `SUM`
* `AVG`
* `COUNT` az eredmény sorainak számát adja meg
* `MIN`
*`MAX`
# Csoportosítás
`SELECT-FROM-WHERE` kifejezést a `GROUP BY` záradékkal folytathatunk, melyet attribútumok listája követ

A `SELECT-FROM-WHERE` eredménye a megadott attribútumok értékei szerint csoportosítódik, az összesítéseket ekkor minden csoportra külön alkalmazzuk
```sql
SELECT * FROM table GROUP BY column1
```
# HAVING
`WHERE` záradék nem alkalmazható összesítő függvényekkel, `HAVING` igen

A `GROUP BY` záradékot egy `HAVING <feltétel>` záradék követheti
Ebben az esetben a feltétel az egyes csoportokra vonatkozik, ha egy csoport nem teljesíti a feltételt, nem lesz benne az eredményben

Az alkérdésre nincs megszorítás
Az alkérdésen kívül ugyanazok a szabályok érvényesek, mint a `SELECT` záradéknál
A `FROM` záradékban megadott relációk bármely attribútumára képezhetünk a `HAVING` záradékban összesítést - Összesítés nélkül a `HAVING` záradékban csak azok az attribútumok fordulhatnak elő, amelyek a `GROUP BY` listában is szerepeltek
A `HAVING` záradékban hivatkozott összesítés csak az éppen feldolgozott csoport soraira vonatkozik
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA3MTE4MTk0MF19
-->