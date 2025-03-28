# B plusz fa
Bináris fák gyorsak, AVL fák méggyorsabbak
Az AVL fa hátránya, hogy annak egy nodeja nem képes kihasználni nagyobb területeket, a fa módosításakor előfordulhat, hogy nagyobb részeket is módosítanunk kellp

A B+ fa optimalizációs megoldás

Például egy $d$-edfokú B+ fa csúcsaiban $4$ bájtos kulcsok és $6$ bájtos pointerek vannak. A B+ fát mágneslemezen tároljuk, ahol a blokkméret $4096$ byte. Mekkorának érdemes választani a $B+$ fa $d$ fokszámát:
$$
4(d-1)+6d\le4096\\
10d\le4100\\
d\le410\\
d:=410
$$
Tehát egy csúcsnak 
## Ábrázolás
A csúcsok mutatokból és kulcsokból állnak, $d$ fokszám
Minden csúcsban legfeljebb $d$ mutató($4\le d$) és $d-1$ kulcs ($d$ állandó, a B+ fa fokszáma)

Az adatokra mutató hivatkozások a levélszinten vannak, a mutatók konkrét adatblokkokra mutatnak
A belső kulcsok hasítókulcsok, tájékozódásban segítenek
### Invariánsok
* Minden belső csúcsban eggyel több mutató van, mint kulcs, ahol $d$ a felső határ a mutatók számára
* Minden $Cs$ belső csúcsra, ahol $k$ a $Cs$ csúcsban a kulcsok száma: az első gyerekhez tartozó részfában minden kulcs kisebb, mint a $Cs$ első kulcsa; az utolsó gyerekhez tartozó részfában minden kulcs nagyobb-egyenlő, mint a $Cs$ utolsó kulcsa; és az $i$-edik gyerekhez tartozó részfában $(2\le i\le k)$ lévő tetszőleges $r$ kulcsra $Cs.kulcs[i-1]\le r\lt Cs.kulcs[i]$
* A gyökércsúcsnak legalább két gyereke van, kivéve ha ez a fa egyetlen csúcsa, következésképpen az egyetlen levele is
* Minden, a gyökértől különböző belső csúcsnak legalább $floor(d/2)$ gyereke van
* Minden levélben legfeljebb $d-1$ kulcs, és ugyanennyi, a megfelelő adatrekordra hivatkozó mutató található
* A gyökértől mindegyik levél ugyanolyan távol található
* Minden levél legalább $floor(d/2)$ kulcsot tartalmaz, kivéve ha a fának egyetlen csúcsa van
* A $B+$ fa által reprezentált adathalmaz minden kulcsa megjelnik valamelyik levélben, balról jobbra szigorúan monoton növekvő sorrendben
## Jelölés
Ha a részfa nem egyetlen levélcsúcsból áll, akkor a következő sémák valamelyike
* $(T_1,k_1,T_2)$
* $(T_1,k_1,T_2,k_2,T_3)$
* $(T_1,k_1,T_2,k_2,T_3,k_3,T_4)$
ahol $T_j$ a $j$-edik részfa $k_j$ pedig a hasító kulcs az $j$-edik és a $j+1$ részfa között
## Beszúrás
Keressük meg a kulcs helyét, ha a levélben már szerepel a kulcs akkor a beszúrás sikertelen
### Van üres hely
Szúrjuk be a megfelelő kulcs/mutató párt kulcs szerint rendezetten ebbe a csúcsba
### Nincs üres hely
Vágjuk szét két csúccsá, és osszuk el a $d$ darab kulcsot egyenlően a csúcs között

Ha a csúcs egy levél, vegyük a második csúcs legkisebb értékének másolatát, és ismételjük meg ezt a beszúró algoritmust, hogy beszúrjuk azt a szülő csúcsába

Ha a csúcs nem levél, vegyük ki a középső értéket, a kulcsok elosztása során, és ismételjük meg  ezt a beszúró algoritmust, hogy beszúrjuk ezt a középső értéket a szülő csúcsba
## Törlés
Keressük meg a kulcsot tartalmazó levelet, ha nincs ilyen a törlés meghiúsult
### A megtalált levélcsúcs egyben gyökércsúcs is
Töröljük a megfelelő kulcsot és a hozzá tartozó mutatót a csúcsból

Ha a csúcs tartalmaz még kulcsot kész vagyunk, különben töröljük a fa egyetlen csúcsát és üres fát kapunk 
### A megtalált levélcsúcs nem gyökércsúcs
Töröljük a megfelelő kulcsot és a hozzá tartozó mutatót a levélcsúcsból

Ha a levélcsúcs még tartalmaz elég kulcsot és mutatót, hogy teljesítse az invariánsokat, kész vagyunk

Ha a levélcsúcsban már túl kevés kulcs van ahhoz, hogy teljesítse az invariánsokat, de a következő, vagy a megelőző testvérének több van, mint amennyi szükséges, osszuk el a kulcsokat egyenlően közte és a megfelelő testvére között
Írjuk át a két testvér közös szülőjében a két testvérhez tartozó hasító kulcsot a két testvér közül a második minimumára

Ha a levélcsúcsban már túl kevés kulcs van ahhoz, hogy teljesítse az invariánst és a következő valamint a megelőző testvére is a minimumon van, hogy teljesítse az invariánst, akkor egyesítsük egy vele szomszédos testvérével
Ennek során a két testvér közül a (balról jobbra sorrend szerinti) másodikból a kulcsokat és a hozzájuk tartozó mutatókat sorban átmásoljuk az elsőbe, annak eredeti kulcsai és mutatói után, majd a második testvért töröljük
Ezután meg kell ismételnünk a törlő algoritmust a szülőre, hogy eltávolítsuk a szülőből a hasító kulcsot (ami eddig elválasztotta a most egyesített levélcsúcsokat), a most törölt második testvérre hivatkozó mutatóval együtt
#### Belső csúcsból való törlés
Töröljük a belső csúcs éppen most egyesített két gyereke közti hasító kulcsot és az egyesítés során törölt gyerekére hivatkozó mutatót a belső csúcsból

Ha a belső csúcsnak van még $floor(d/2)$ gyereke, (hogy teljesítse az invariánsokat) kész vagyunk

Ha a belső csúcsnak már túl kevés gyereke van ahhoz, hogy teljesítse az invariánsokat, de a következő vagy a megelőző testvérének több van, mint amennyi szükséges, osszuk el a gyerekeket és a köztük levő hasító kulcsokat egyenlően közte és a megfelelő testvére között, a hasító kulcsok közé a testvérek közti (a közös szülőjükben lévő) hasító kulcsot is beleértve
A gyerekek és a hasító kulcsok újraelosztása során, a középső hasító kulcs a testvérek közös szülőjében a két testvérhez tartozó régi hasító kulcs helyére kerül úgy, hogy megfelelően reprezentálja a köztük megváltozott vágási pontot! (Ha a két testvérben a gyerekek összlétszáma páratlan, akkor az újraelosztás után is annak a testvérnek legyen több gyereke, akinek előtte is több volt

Ha a belső csúcsnak már túl kevés gyereke van ahhoz, hogy teljesítse az invariánst, és a következő, valamint a megelőző testvére is a minimumon van, hogy teljesítse az invariánst, akkor egyesítsük egy vele szomszédos testvérével
Az egyesített csúcsot a két testvér közül a (balról jobbra sorrend szerinti) elsőből hozzuk létre. Gyerekei és hasító kulcsai először a saját gyerekei és hasító kulcsai az eredeti sorrendben, amiket a két testvér közti (a közös szülőjükben lévő) hasító kulcs követ, és végül a második testvér gyerekei és hasító kulcsai jönnek, szintén az eredeti sorrendben. Ezután töröljük a második testvért
A két testvér egyesítése után meg kell ismételnünk a törlő algoritmust a közös szülőjükre, hogy eltávolítsuk a szülőből a hasító kulcsot (ami eddig elválasztotta a most egyesített testvéreket), a most törölt második testvérre hivatkozó mutatóval együtt
#### Gyökércsúcsból való törlés, ha az nem levélcsúcs
Töröljük a gyökércsúcs éppen most egyesített két gyereke közti hasító kulcsot és az egyesítés során törölt gyerekére hivatkozó mutatót a gyökércsúcsból

Ha a gyökércsúcsnak van még 2 gyereke, kész vagyunk

Ha a gyökércsúcsnak csak 1 gyereke maradt, akkor töröljük a gyökércsúcsot, és a megmaradt egyetlen gyereke legyen az új gyökércsúcs
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMDI3MTMzNzVdfQ==
-->