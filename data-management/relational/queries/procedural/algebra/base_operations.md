Algebra általában műveleteket és atomi operandusokat tartalmaz

A relációs algebra lehetővé teszi kifejezések megfogalmazását az atomi operandusokon és az algebrai kifejezéseken végzett műveletek alkalmazásával kapott relációkon

Minden művelet végeredménye reláció, amelyen további műveletek adhatók meg

**Változó** és **konstans** operandusok

Egy relációkon értelmezett operátor akkor **monoton**, ha bármelyik argumentumrelációhoz egy újabb sort hozzávéve az eredmény tartalmazza az összes olyan sort, amelyet addig tartalmazott és esetleg újabb sorokat is
# Műveletek
## Projekció (Projection)
Kiválasztja a reláció alsó indexű attribútumait.
$$
\sqcap_{A1,...,Ak}(R)
$$
> `SELECT A1,...,Ak FROM R`
## Kiválasztás (Selection)
Kiválasztja az adott relációból azokat a sorokat, amelyek megfelelnek egy bizonyos feltételnek.
$$
\sigma_{F}(R)
$$
> `SELECT * FROM R WHERE C`;
## Átnevezés (Rename)
Átnevezi az attribútumokat vagy a relációt.
$$
\rho_{X/Y}(R)
$$
> `SELECT A AS X, B AS Y FROM R;`

> `SELECT * FROM R AS X;`
## Unió (Union)
Összefésüli két relációt, hogy létrehozzon egy újat, ami tartalmazza mindkét bemeneti reláció sorait.
$$
R\cup S
$$
> `SELECT * FROM R UNION SELECT * FROM S`
## Különbség (Difference)
Kiszámolja két reláció különbségét, azaz a sorokat, amelyek csak az első relációban szerepelnek.
$$
R\backslash S
$$
> `SELECT * FROM R MINUS SELECT * FROM S`
## Descartes-szorzat (Cartesian Product)
Létrehoz egy új relációt, amely tartalmazza minden lehetséges párt a két bemeneti reláció sorai között.
$$
R\times S
$$

> `SELECT * FROM R,S`
# Logikai műveletek
## Konjukció
A lekérdezés csak azokat a rekordokat adja vissza, amelyekre mind a két feltétel igaz
## Diszjunkció
A lekérdezés azokat a rekordokat adja vissza, amelyek legalább az egyik feltételnek megfelelnek
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ0NDY3MzMyMV19
-->