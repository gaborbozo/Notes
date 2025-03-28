Egy $R(A_1,...,A_n)$ **reláció redundáns**, ha valamely $A_i$ attribútum éréték ki tudjuk az $\{A_j\vert j\ne i\}$ attribútumok értékeiből "következtetni"
# Funkcionális függőségek
Adott adatmező értéke meghatározott egyéb adatmező értékétől függ

$X\rarr Y$ egy $R$ relációra vonatkozó megszorítás, miszerint ha két sor megegyezik $X$ összes attribútumán, $Y$ attribútumain is meg kell, hogy egyezzenek

$X\rarr A_1A_2…A_n$ akkor és csak akkor teljesül $R$ relációra, ha $X->A1,X->A2,…, X->A_n$ is teljesül $R$-en
>$A\rarr BC=A\rarr B\land A\rarr C$
>name $\rarr$ address,favouriteTea $=$ name $\rarr$ address $\land$ name$\rarr$ favouriteTea

$K$ **szuperkulcs** $R$ relációra, ha $K$ funkcionálisan meghatározza $R$ attribútumait
$K$ **kulcs** $R$-en, ha $K$ szuperkulcs, de egyetlen valódi részhalmaza sem szuperkulcs
>Bosses(name,adress,favouriteTea,producer,likedTeas)
>$\{$name,likedTeas$\}$ szuperkulcsok
>name $\rarr$ address,favouriteTea
>likedTeas $\rarr$ producer
>$\{$name,likedTeas$\}$ kulcs, hiszen sem $\{$név$\}$, sem $\{$kedveltTeák$\}$ nem szuperkulcs
>name $\rarr$ producer, likedTeas $\rarr$ address, nem teljesül
## Armstrong-axiómák
* **Reflexitivitás**: ha $Y\subseteq X\subseteq R$, akkor $X\rarr Y$ (triviális függőségek)
* **Bővítés**: ha $X\rarr Y$ teljesül, akkor tetszőleges $Z\subseteq R$-ra $XZ\rarr YZ$ teljesül
* **Tranzitivitás**: ha $X\rarr Y\land Y\rarr Z$, akkor $X\rarr Z$
## Lezárt (closure)
Adott $R$ reláció és $F$ FF halmaza mellett, $Y$ lezártja $(Y^+)$ az összes olyan $A$ attribútum halmaza, amire $Y\rarr A$ következik $F$-ből
#### Algoritmus
1. Kiindulás: $Y^+=Y$
2. Indukció: Olyan $FF$-ket keresünk, melyeknek a baloldala már benne van $Y^+$-ban, ha $X\rarr A$ ilyen, $A$-t hozzáadjuk $Y^+$-hoz
2. Ha $Y^+$-hoz már nem lehet további attribútumot adni, vége
>Adott $R$ tartalmazza az $A$ attribútumokat, és adottak $F=\{A\rarr B,B\rarr C,C\rarr D\}$ FF-ek
> Az $A^+$ az összes olyan attribútum halmaz, amelyeket az $A$ attribútumokból az $F$ FF-ek alapján levezethetünk
>
>$A^+=\{A,B,C,D\}$
## Exponenciális algoritmus
1. Minden $X$ attribútumhalmazra számítsuk ki $X^+$ -t
2. Adjuk hozzá a függőségeinkhez $X\rarr A$-t minden $A$-ra $X^+-X$ -ből
3. Dobjuk ki $XY\rarr A$-t, ha $X\rarr A$ is teljesül ($XY\rarr A$ az $X\rarr A$-ból minden esetben következik
4. Végül csak azokat az FF-ket használjuk, amelyekben csak a projektált attribútumok szerepelnek
* Az üreshalmaznak és az összes attribútum halmazának nem kell kiszámolni a lezártját
* Ha $X^+=$ az összes attribútum, akkor egyetlen $X$- t tartalmazó halmaznak sem kell kiszámítani a lezártját
>$A,B,C\land F=\{A\rarr B,B\rarr C\}$
>$A^+=ABC;A\rarr B,A\rarr C$
>$B^+=BC;B\rarr C$
>$C^+=C$
>$BC^+=BC$
> 
>$A\rarr C$-re projektálunk: $\{A\rarr C\}$
## Anomáliák
Az anomáliák olyan problémák az adatbázisok tervezése során, amelyek hibás adatokhoz és inkonzisztenciákhoz vezethetnek
* A **módosítási anomália** akkor jelentkezik, ha egy adott adatot több helyen tárolunk, és amikor módosítjuk azt, nem frissítjük az összes helyen
* A **törlési anomália** akkor jön létre, ha egy adatot több helyen tárolunk, és amikor töröljük azt egy helyen, az összes más helyen is törölnünk kell
* A **beszúrási anomália** akkor fordul elő, ha nem lehet egy adatot felvenni, mert az adat egy másik attribútumtól függ
## Veszteségmentes  felbontás
Adott $R$ reláció attribútumainak részhalmazai $(R_1,...,R_k)$ úgy vannak összekapcsolva, hogy az eredeti adatok teljesen visszaállíthatók az összekapcsolás után
Más szóval, nincs adatvesztés az összekapcsolás során, és az eredeti adatokat pontosan úgy lehet rekonstruálni ahogyan előtte voltak
## Boyce-Codd normálforma
$R$ reláció $BCNF$ normálformában van, ha minden $X\rarr Y$emtriviális FF-re $R$-ben $X$ szuperkulcs
* Nemtriviális: Y nem része X-nek
* Szuperkulcs: tartalmaz kulcsot (ő maga is lehet kulcs)
#### Felbontás
Adott $R$ reláció és $F$ funkcionális függőségek
Van-e olyan $X\rarr Y$ FF, ami sérti a BCNF-t? Ha van olyan következmény FF F-ben, ami sérti a BCNF-t, akkor egy F-beli FF is sérti

Kiszámítjuk $X^+$-t
Ha itt nem szerepel az összes attribútum, $X$ nem szuperkulcs.
#### R dekomponálása X -> Y felhasználásával
$R$-t helyettesítsük az alábbiakkal
1. $R_1=X^+$
2. $R_2=R–(X^+–X)$

Projektáljuk a meglévő $F$-beli FF-eket a két új relációsémára
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Njc0MTcwNDldfQ==
-->