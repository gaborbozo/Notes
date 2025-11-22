A **tranzakció** olyan folyamat, ami adatbázis lekérdezéseket, módosításokat tartalmaz
Az utasítások egy értelmes egészt alkotnak
Egyetlen utasítást tartalmaznak, vagy az SQL-ben explicit módon megadhatóak
Végrehajtásuk tartós

#### Tranzakciók feldolgozása két nagyobb részből áll
**Konkurenciakezelő**: tranzakciók oszthatatlanságára, elkülönítésére
* Egy táblában ugyanazt a rekordot egyidőben ketten változtatják. Hogyan tudjuk elkerülni a versenyhelyzetet?

**Naplózás- és helyreállítás-kezelő**: tranzakciók tartósságára
* Egymillió forintot utalunk bankfiókok között, de áramkimaradás van. Mi a korrekt adatbázis állapot?
# ACID tranzakciók
* Atomiság (atomicity): vagy az összes vagy egy utasítás sem hajtódik végre 
* Konzisztencia (consistency): az adatbázis megszorítások megőrződnek
* Elkülönítés (isolation): a felhasználók számára úgy tűnik, mintha folyamatok, elkülönítve, egymás után futnának le
* Tartósság (durability): egy befejeződött tranzakció módosításai nem vesznek el

A **COMMIT** SQL utasítás végrehajtása után a tranzakció véglegesnek tekinthető

A **ROLLBACK** SQL utasítás esetén a tranzakció abortál, az összes utasítás visszagörgetésre kerül
A $0$-val való osztás vagy egyéb hibák, szintén visszagörgetést okozhatnak, akkor is, ha a programozó erre nem adott explicit utasítást

> **Egymással átfedésben álló utasításokra** példa, ha Joe árul két teát és Sally tudni akarja a legdrágább és a legolcsóbb tea árát is
> Sally lekérdezi a legolcsóbbat és legdrágábbat (egyidőben), viszont a két művelet között Joe törli a tábla tartalmát és beszúr egy új elemet
> Ekkor Sally nem valós, a régi állapotnak megfelelő adatot is kap
> Megoldás ha Sally utasításait egy tranzakcióba gyűjtjük ezzel kikerülve az inkinzisztenciát

> **Visszagörgetés alapú hibaforrásra** példa, ha Joe a törlés és beszúrás utasításokat nem, mint tranzakció hatja végre, viszont utána úgy dönt, jobb ha visszagörgeti a módosításokat
> Ha Sally a beszúrás után, de a visszagörgetés előtt hajtja végre a tranzakciót, olyan értéket kap ami végül nincs is benne az adatbázisban
> Megoldás ha Joe a két utasítást mint tranzakció hajtja végre, így a változtatások akkor válnak láthatóvá, ha a tranzakció egy COMMIT utasítást hajt végre
## Elkülönítési szintek
Az SQL négy elkülönítési szintet definiál, amelyek megmondják, hogy milyen interakciók engedélyezettek az egy időben végrehajtódó tranzakciók közt

Elkülönítési szint megválasztása `SET TRANSACTION ISOLATION LEVEL [SERIALIZABLE|REPEATEBLE READ|READ COMMITTED|READ UNCOMMITTED]`
Ez a döntés csak azt adja meg, hogy mi hogyan látjuk az adatbázist

* A `READ UNCOMMITTED` elkülönítési szinten futó tranzakció akkor is láthatja az adatokat, amikor a változtatások még nem lettek véglegesítve (kommitolva), piszkos adatok
* `READ COMMITTED` szinten csak a kommitálás utáni adat látható, de nem feltétlen mindig ugyanaz az adat, nem ismételhető olvasás
* `REPEATABLE READ` hasonló a `READ COMMITTED`-hez, viszont itt ha az adatot újra beolvassok, akkor amit előszor láttunk, másodszor is látni fogjuk
* `SERIALIZABLE` esetén az adatbázist módosító utasítás előtt vagy után láthatjuk, közben sohasem

| Elkülönítési szint | Piszkos adat olvasása | Nem ismételhető olvasás | Fantomadatok |
|--|--|--|--|
| `READ UNCOMMITTED` | Megengedett | Megengedett | Megengedett |
| `READ COMMITTED` | Nem megengedett | Megengedett | Megengedett |
| `REPEATABLE READ` | Nem megengedett | Nem megengedett | Megengedett |
| `SERIALIZABLE` | Nem megengedett | Nem megengedett | Nem megengedett |
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc3Mzk3MjY1NF19
-->