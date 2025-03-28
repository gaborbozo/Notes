**Költségmodell** a kiszámítás költsége arányos a relációs algebrai kifejezés részkifejezéseinek megfelelő relációk tárolási méreteinek összegével.
**Módszer** a műveleti tulajdonságokon alapiló ekvivalens átalakításokat alkalmazunk, hogy várhatóan kisebb méretű relációk keletkezzenek.
**Heurisztikus eljárás** hiszen nem az argumentum relációk valódi méretével számol, ugyanakkor nem is egyértelmű mert az átalakítások sorrendje nem determinisztikus, így más sorrendben végrehajtva az átalakításokat más végeredményt kaphatunk, de midnegyik általában jobb költségű, mint a kiindulási pont.

## Kifejezésfa
> Relációs algebrai kifejezést gráffal ábrázolunk.

A **nem levél csúcsok** a relációs algebrai műveletek.
* **unáris** $\Big(\sigma,\prod,\rho\Big)$
* **bináris** $\Big(\backslash,\cup,\times\Big)$

A **levél csúcsok** konstans telációk vagy relációs változók.
## Alap algebrai operációk szabályai
### Kommutativitás
* Szorzás $(\times)$
* Természetes összekapcsolás $(\vert\times\vert)$
* Théta-összekapcsolás $\Big(\begin{array}{c}\vert\times\vert\\\Theta \end{array}\Big)$
$$S\cdot R\approxeq R\cdot S$$
### Asszociativitás
* Szorzás
* Természetes összekapcsolás
* Théta-összekapcsolás
$$
(R\cdot S)\cdot T\approxeq R\cdot(S\cdot T)
$$
### Vetítések összevonása, bővítése
$A$ és $B$ két részhalmaza az $S$ relácó oszlopainak úgy, hogy $A\subseteq B$.
$\prod_A\big(\prod_B(S)\big)\approxeq\prod_A(S)$
### Kiválasztások felcseréhetősége, felbontása
$F_1,F_2$ az $S$ reláció oszlopain értelemzett kiválasztási feltétel.
$$
\sigma_{F_1\land F_2}(S)\approxeq\sigma_{F_1}\big(\sigma_{F_2}(S)\big)\approxeq\sigma_{F_2}\big(\sigma_{F_1}(S)\big)
$$
### Kiválasztás és vetítés felcserélhetősége
$F$ az $S$ relációnak csak az $A$ oszlopain értelmezett kiválasztási feltétel.
$\prod_A\big(\sigma_F(S)\big)\approxeq\sigma_F\big(\prod_A(S)\big)$
### Kiválasztás és szorzás felcserélhetősége
$F$ az $S$ reláció oszlopainak egy részhalmazán értelmezett kiválasztási feltétel.
$$
\sigma_F(S\times R)\approxeq\sigma_F(S)\times R
$$
> Speciálisan ha $i=1,2,Fi$ az $S$ és $R$ relációk oszlopainak egy részhalmazán értelmezett konjunkció, illetve $F=F_1\land F_2$.
> $$
> \sigma_F(S\times R)\approxeq\sigma_{F1}(S)\times\sigma_{F2}(R)
> $$
### Kiválasztás és egyesítés felcserélhetősége
$S,R$ relációk sémája megegyező, és $F$ a közös sémán értelmezett kiválasztási feltétel.
$$
\sigma_F(S\cup R)\approxeq\sigma_F(S)\cup\sigma_F(R)
$$
### Kiválasztás és kivonás felcserélhetősége
$S,R$ relációk sémája megegyező, és $F$ a közös sémán értelmezett kiválasztási feltétel.
$$
\sigma_F(S\backslash R)\approxeq\sigma_F(S)\backslash\sigma_F(R)
$$
### Kiválasztás és természetes összekapcsolás felcserélhetősége
$F$ az $S$ és $R$ közös oszlopainak egy részhalmazán értelmezett kiválasztási feltétel.
$$
\sigma_F(S\vert\times\vert R)\approxeq\sigma_F(S)\vert\times\vert\sigma_F(R)
$$
### Vetítés és szorzás felcserélhetősége
$i=1,2$ esetén az $A_i$ az $S$ és $R$ relációk oszlopainak egy halmaza, valamint legyen $A=A_1\cup A_2$.
$\prod_A(S\times R)\approxeq\prod_{A_1}(S)\times\prod_{A_2}(R)$
### Vetítés és egyesítés felcserélhetősége
$S,R$ relációk sémája megegyező, és legyen $A$ a sémában szereplő oszlopok egy részhalmaza.
$\prod_A(S\cup R)\approxeq\prod_A(S)\cup\prod_A(R)$
## Optimalizációs heurisztikus elvei
* Minél hamarabb szelektáljunk.
* Próbáljunk természetes összekapcsolásokat képezni, ugyanis ezek hatákonyabban kiszámolhatóak, mint a szorzatból történő kiválasztás.
* Vonjuk össze az egymás utáni unáris műveleteket (kiválasztások és vetítések), amelyekből lehetőleg egy műveletet képezzünk.
* Közös részkifejezések keresése, amiket így elég csak egyszer kiszámolni.
*
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIzNjE0Njk4OF19
-->