Data Definition Language (DDL)

Segítségével hozhatunk létre adatobjektumokat, deklarálhatunk megszorításokat stb.
# CREATE
```sql
CREATE TABLE <name> (
		<item_list_1>,
		..
		<item_list_n>
	)
```
## Típusok
* `INT`/`INTEGER`
* `REAL`/`FLOAT`
* `CHAR(n)` rögzített hosszúságú string, $n$ hosszú
* `VARCHAR(n)` változó hosszúságú string, legfeljebb $n$ hosszú
* `DATE` $(yyyy-mm-dd)$
* `TIME` $(hh:mm:ss)$
## Megszorítások
### Attribútum alapú
Attribútum-alapú ellenőrzést csak beszúrásnál és módosításnál hajt végre a rendszer
`CHECK(<condition>)` hozzáadása az attribútum deklarációjához
```sql
CREATE TABLE Servers(
	shop CHAR(20),
	tea CHAR(20), CHECK (tea IN (SELECT name FROM Teas)),
	price REAL CHECK (price <= 1500.0)
);
```
### Sor alapú
Sor alapú ellenőrzést csak beszúrásnál és módosításnál hajt végre a rendszer
`CHECK (<condition>)` megszorítás a séma elemeként
Feltétben tetszőleges oszlop és reláció, viszont más relációk attribútumai csal alkérdésben jelenhetnek meg
```sql
CREATE TABLE Serves(
	shop CHAR(20),
	tea CHAR(20),
	price REAL,
	CHECK (shop = ’Joe's tea shop’ OR price <= 1500.00)
);
```
### Globális
Adatbázissémához tartoznak
`CREATE ASSERTION <name> CHECK (<condition>);`
A feltétel tetszőleges táblára és oszlopra hivatkozhat az adatbázissémából

Az adatbázis bármely módosítása előtti ellenőrzés
Felismeri, hogy mely változtatások, mely megszorításokat érinthetnek
```sql
CREATE ASSERTION OnlyLowPrice CHECK(
	NOT EXISTS(
		SELECT name FROM Serves
		GROUP BY shop
		HAVING 1500.00 < AVG(price)
));
```
## Kulcsok
* `UNIQUE` minden rekord egyedi azonosítóját határozza meg
* `PRIMARY` `UNIQUE` kulcs, amely a táblában lévő adatok azonosítására és összekapcsolására szolgál
Nem lehet `NULL`
* `FOREIGN` egy tábla főkulcsára mutató másik mező
* `COMPOSITE` két vagy több mezőből áll, és együttesen azonosítanak egy rekordot. Segítségével lehetőség van azonosítani egy rekordot több mező alapján 
* `SUPER`
## Idegen kulcsok
Egy reláció attribútumainak értékei egy másik reláció értékei között is meg kell, hogy jelenjenek együttesen

`FOREIGN KEY (<attribute list>) REFERENCES <relation> (<attributes>) `
```sql
CREATE TABLE Teas(
	name CHAR(20) PRIMARY KEY, 
	manufacturer CHAR(20)
); 

CREATE TABLE Serves(
	shop CHAR(20),
	tea CHAR(20) REFERENCES Teas(name),
	price REAL
);
-- OR
CREATE TABLE Serves(
	shop CHAR(20),
	tea CHAR(20),
	price REAL
	FOREIGN KEY(tea) REFERENCES Teas(name)
);
```
### Megszorítások megőrzése
Egy idegen kulcs megszorítás $R$ relációról $S$ relációra kétféleképpen sérülhet
* Egy $R$-be történő beszúrásnál $S$-ben nem szereplő értéket adunk meg
* Egy $S$ beli törlés „lógó” sorokat eredményez $R$-ben

Védekezésükre megoldás lehet
* `DEFAULT` érték meghatározása 
* **Továbbgyűrűzés**
Töröljük azokat az idegen kulcsokkal ellátott elemeket amik a törölt, elsődleges kulcsra hivatkoznak
* `SET NULL`
A továbbgyűrűzéssel ellentétben itt a kulcsra hivatkozó sorok értékét `NULL`-ra állítjuk
#### Stratégia deklarálása
`[UPDATE,DELETE][SET NULL,CASCADE]`
```sql
CREATE TABLE table_name(
	attribute ...
	FOREIGN KEY (value)
		REFERENCES reference_table(value)
		ON DELETE SET NULL
		ON UPDATE CASCADE
);
```
# DROP
```sql
DROP TABLE <name>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3ODc3ODc5M119
-->