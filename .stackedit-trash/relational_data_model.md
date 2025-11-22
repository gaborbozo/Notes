A **relációs adatmodell** egy matematikai modell, amely az adatokat kétdimenziós, táblázatos formában reprezentálja amelyeket relációként ismerünk

A reláció fejrészében találhataók az **attribútumok**
Minden attribútumhoz tartozik egy **értékkészlet**

**Relációséma** áll a reláció nevéből és a reláció-attribútumok halmazából
A reláció attribútimainak sorrendje felcserélhető

A **séma** egy adatmodellben általánosságban azt adja meg, hogy egy-egy adatelem milyen "formájú" adatokat tárol

Egy-egy reláció soroknak egy halmaza(nem számít a sorrend, illetve egy elem csak egyszer szerepelhet)
A reláció sorainak halmazát **előfordulásnak** nevezzük

Két reláció azonos ha az attribútumok nevükben igen, viszont tartalmukban nem térnek el, illetve ha $A$ és $B$ táblában az adatok megegyeznek, legfeljebb az egyes sorok "indexei" térnek el egymástól

Az adatbázis relációk halmaza. A megfelelő relációsémák halmaza adja az **adatbázissémát**, a hozzátartozó előfordulások pedig az **adatbázis-előfordulást**

Egy sor elemeit **mezőnek** (komponens) nevezzük
Minden mező csak atomi értéket vehet fel
# Megszorítások (Constraint)
Az attribútumok egy halmaza egy **kulcsot** alkot egy relációra nézve, ha a reláció bármely előfordulásában nincs két olyan sor, amelyek a kulcs összes attribútumának értékein megegyeznének
Olyan szabályok vagy feltételek, amelyeket azért alkalmazunk, hogy biztosítsuk az adatok integritását és konzisztenciáját - helytelen rekordok létrejöttének megakadályozása

Egy Kulcs nem feltétlenül egy attribútumból áll

A megszorításokat a tábla létrehozásakor tudjuk definiálni

**Hivatkozási épségről** beszélünk ha egy érték megjelenik valahol egy környezetben, akkor ugyanez az érték egy másik, az előzővel összefüggő környezetben is meg kell, hogy jelenjen.
> Például a Tea(név, ország), Felszolgál(tea, teázó, ár) táblák esetén megköveteljük, hogy csak olyan teák szerepeljenek a Felszolgál táblában, amelyek a Tea táblában is szerepelnek
> 
>  A megszorítás: $\varPi_{tea}(Felszolgál)\subseteq\varPi_{név}(Tea)$
**Egységességről** beszélünk ha egy adott adattípusú adatok egy adott oszlopban egyformának kell lenniük
> Például, ha egy oszlopban dátumokat , akkor biztosítja, hogy az összes adat az adott oszlopban dátumként legyen tárolva.
## Elsődleges kulcs (Primary key)
Az elsődleges kulcs egy olyan érték, amely alapján minden rekord egyértelműen és összetéveszthetetlenül beazonosítható
> `CREATE TABLE table (column1 type NOT NULL, column2 type NOT NULL, PRIMARY KEY (column1,column2))`
## Idegen/Másdoglagos kulcs (Foreign key)
A másodlagos kulcs egy olyan oszlop vagy több oszlop, amely kapcsolatot biztosít két tábla adatai között
Az idegen kulcs egy olyan azonosító, amellyel egy másik tábla elsődleges kulcsára hivatkozhatunk
> `CREATE TABLE table2 (column type, FOREIGN KEY (column) REFERENCES table1(primary_key))`
## Egyedüli érték megszorítások (Unique)
Az egyedüli érték megszorítások biztosítják, hogy az adatok egy adott oszlopban csak egyszer fordulnak elő
> `CREATE TABLE table (column type NOT NULL, UNIQUE(column))`
## Null érték megszorítások (Not null)
A null érték megszorítások biztosítják, hogy az adatbázisban ne lehessen null értékű adatokat tárolni azon az oszlopon, amelyen a megszorítás alkalmazására került sor

> `CREATE TABLE table (column type NOT NULL)`
## Ellenőrző megszorítások (Check)
Az ellenőrző megszorítás azt biztosítja, hogy az oszlopokban lévő adatok megfelelnek egy meghatározott feltételnek vagy feltételrendszernek
> `CREATE TABLE table(column type NOT NULL, CHECK (condition))`
## Default megszorítások
Ez a megkötés meghatároz a mezők számára egy alapértelmezett értéket, akkor kerül felhasználásra, ha a felhasználó új rekord felvételekor nem határozott meg értéket a mező számára
> `CREATE TABLE table(column type DEFAULT value)`
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM0NDEwNzI2NF19
-->