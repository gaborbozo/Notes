Data Manipulation Language (DML)

Nem adnak vissza eredményt
# Insert
```sql
INSERT INTO <relation>
VALUES (<attribute list>)

INSERT INTO <relation>(column_1,..,column_n)
VALUES (value_1,..,value_n)
```
Opcionálisan megadhatóak az attribútumok egyenként
* ha nem a sorrendnek megfelően szeretnénk beszúrni azokat
* Nincs minden attribútumnak értéke. A hiányzó értékek vagy `NULL` vagy `DEFAULT` értékkel helyettesítődnek

Lekérdezés eredményének beszúrása
```sql
INSERT INTO <relation>
(<alkérdés>)
```
# Delete
```sql
DELETE FROM <relation>
WHERE <condition>

-- összes sor törlése
DELETE FROM <relation>
```
# Update
Bizonyos sorok bizonyos attribútumainak módosítása
```sql
UPDATE <relation>
SET <attribute_1=value_1,..,attribute_n=value_n>
WHERE <condition>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYxNjU0NDYwMl19
-->