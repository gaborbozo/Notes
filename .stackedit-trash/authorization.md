Összességében $9$ jogosultság
A felhasználókat egy jogosultsági azonosító (authorization ID) alapján azonosítjuk, általában ez a bejelentkezési név
A magunk készítette objektumok esetében az összes jogosultsággal rendelkezünk

#### Jogosultságok megadásának szintaktikája
```sql
GRANT <list of privileges>
ON <relation or other type of object>
TO <list of authorization IDs>
```
A `WITH GRANT OPTION` utasításrész hozzáadásával lehetőve tesszük, hogy aki megkapta a jogosultságot, tovább is adhassa azt

```sql
-- Sally lekérdezhet a táblából és
-- módosíthatja a price attribútum halmazt

GRANT SELECT, UPDATE(price)
ON Serves
TO Sally
```
#### Jogosultsáok visszavonásának szintaktikája
```sql
REVOKE <list of privileges> 
ON <relation or other type of object>
FROM <list of authorization IDs>
```
A `REVOKE` utasításhoz a két opció közül valamelyiket még hozzá kell adnunk
* `CASCADE` azok a jogosultságok, melyeket az adott ki a visszavonandó jogosultságon keresztül, akitől éppen visszavonjuk az adott jogosultságot, szintén visszavonódnak
* `RESTRICT` a visszavonás nem hajtódik végre, amíg a visszavonandó jogosultságtól függő jogosultságok is vannak
Először ezeket kell megszüntetni
<!--stackedit_data:
eyJoaXN0b3J5IjpbODIyODI3MTE1XX0=
-->