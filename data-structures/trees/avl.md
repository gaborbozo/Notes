# AVL fák
Magasság szerint kiegyensúlyozott bináris keresőfák

Egy bináris fa egy $*p$ csúcsa kiegyensúlyozott, ha a csúcs $p\rarr b$ egyensúlyára(balance) $\vert p\rarr b\vert\le1$
$$
p\rarr b=h(p\rarr right)-h(p\rarr left)
$$ 

Tetszőleges $n$ csúcsú AVL fa $h$ magasságára igaz, hogy
$$
[\log n]\le h\le 1,45\log n,\text{ azaz }h\in\Theta(\log n)
$$
## Ábrázolás
Láncoltan történik
* A csúcsokban a $b$ egyensúly attribútumot expliciten tároljuk
	* `b`$\in\{-1,0,1\}$
* Másik implementáció, hogy a két részfa magasságainak tárolása
* Másik implementáció, hogy csak az aktuális részfa magasságát tárolja
### Csúcsok jelzői $b$ egyensúly attribútum implementáció
* $=$ vagy $0$, ha a csúcs két részfájának magassága egyenlő
* $-$, ha a csúcs baloldali részfájának magassága eggyel nagyobb, mint a jobboldali részfa magasaggáa
* $+$ ...
## Jelölés
`bal_részfa gyökér b jobb_részfa`
pl `{ [2] 4+ [ (6) 8= (10) ] }`

A levelek csúcsai mindig $0$ ezért azt nem tüntetjük fel
## Forgatási sémák
Beszúrás esetén négy lehetséges eset
* $(++,+)$
* $(++,-)$
* $(--,-)$
* $(--,+)$

Törlés esetén az előbbi, plusz még kettő
* $(++,0)$
* $(--,0)$
## Beszúrás
* Rekurzív módon megkeressük a beszúrandó elem helyét
* Ha megtaláltuk akkor beszúrjuk és $d$ értékét igazra állítjuk
* A rekurzió miatt visszafelé minden csúcs esetén addig forgatunk amíg $d$ igaz
## Törlés
* Rekurzív módon megkeressük a törlendő elemet
* Töröljük az elemet, ezután lehetséges, hogy
  * A törlendő csúcsnak nincs bal gyereke, ekkor a helyét a jobb veszi át
  * A törlendő csúcsnak nincs jobb gyereke, ekkor a helyét a bal veszi át
  * A törlendő csúcsnak jobb és bal gyereke is van, ekkor a jobb részfa mininmuma kerül a helyére
* A rekurzió miatt visszafelé minden csúcs esetén addig forgatunk amíg $d$ igaz
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMwMTY5MTU5MV19
-->