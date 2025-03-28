# Egyszerű gráfok
$G=(V,E)$ rendezett páros, ahol $V$ a csúcsok tetszőleges véges halmaza, $E\subseteq V\times V\backslash\{(u,u):u\in V\}$ (párhuzamos és hurokélek kizárása) pedig az élek halmaza

$V=\{\}$ üres gráf, $V\ne\{\}$ nem üres gráf

A $G=(V,E)$ gráf irányítatlan, ha tetszőleges $(u,v)\in E$ élre $(u,v)=(v,u)$

A $G=(V,E)$ gráf irányított, ha tetszőleges $(u,v),(v,u)\in E$ élpárra $(u,v)\ne(v,u)$. Ekkor azt mondjuk, hogy az $(u,v)$ él fordítottja a $(v,u)$ él

A **DAG** (directed acyclic graph) alatt irányított, körmentes gráfot értünk
## Gráfábrázolás
$G=(V,E), V=\{1,..,n\},n=\vert V\vert, 1..n$
A gráf egyértelműen azonosítható csúcsai
### Grafikus
#### Irányítatlan
$a-b$ azt jelzi, hogy létezik $a$ és $b$ között vonal, közvetlen kapcsolatban vannak egymással

$a-b;c$ rövidítése $a-b,a-c$-nek
#### Irányított
$1\rarr2$
$1\rarr2;3$
### Szöveges
#### Irányítatlan
$u-v_{u_1};...;v_{u_k}$ azt jelenti, hogy az $u$ csúcsnak szomszédai a $v_{u_1},...,v_{u_k}$ csúcsok, azaz $(u,v_{u_1}),...,(u,v_{u_k})$ élei a gráfnak
#### Irányított
$u\rarr v_{u_1};...;v_{u_k}$ azt jelenti, hogy a gráfban az $u$ csúcsból az $(u,v_{u_1}),...,(u,v_{u_k})$ irányított élek indulnak ki
### Csúcsmátrixos reprezentáció
$G=(V,E)$ gráfot egy $A/1:bit[n,n]$ mátrix reprezentálja, ahol $n=\vert V\vert$ a csúcsok száma, $1..n$ a csúcsok sorszámai

$bit=\{0,1\}$
$A[i,j]=1\Rarr (v_i,v_j)\in E$
$A[i,j]=0\Rarr (v_i,v_j)\notin E$

$A[i,i]$ hurokél
#### Irányítatlan
| $A$ | $1$ | $2$ | 
|--|--|--|
| $1$ | $0$ | $1$ |
| $2$ | $1$ | $0$ |
Alapján $1$ és $2$ között van vonal

Tárigény csökkentése érdekében elég egy alsó- vagy felsőháromszög mátrixot felrajzolni, ugyanis oda-vissza irányról nem beszélünk

$B:bit[n(n-1)/2]$
$A[i,j]=B[(i-1)(i-2)/2+(j-1)]$, ha $i\gt j$ - alsóháromszög mátrix
$A[i,j]=A[j,i]$, ha $i\lt j$ - felsőháromszög mátrix
#### Irányított
| $A$ | $1$ | $2$ | 
|--|--|--|
| $1$ | $0$ | $1$ |
| $2$ | $0$ | $0$ |
Alapján $1$-ből mutat $2$-be egy vonal
### Szomszédossági listás
$A/1:Edge*[n]$ pointertömb segítségével ábrázoljuk ami 
* `v` $(v\in\N)$
* `next` (Edge pointer)
#### Irányítatlan
A pointertömb $i$-edik eleme tartalmazza az $i$ edik csúcs szomszédait
Egy kapcsolatot a tömb mind a két elemében jeleznünk kell
#### Irányított
A pointertömb $i$-edik eleme tartalmazza az $i$ edik csúcs gyerekeit

$A[1]->v=3;A[1]->next->v=4;A[1]->next->next->0$
$A[4]$
Jezi azt a gráfot ahol $1$ mutat $3$-ba és $4$-be, és $4$ nem mutat semmibe
## Reprezentáció választás
### Élek számának függvényében
Ha $m\lt\lt n^2$, akkor **éllistás**
* gráf ritka
* mátrix kihasználhatatlan
* síkgráf

Ha $m$ megközelíti $n^2$-et akkor **csúcsmátrixos**
* gráf sűrű
* túl hosszű éllisták
## Műveletigény
$G=(V,E),n=\vert V\vert,m=\vert E\vert$
$0\le m\le n*n(n-1)\le n^2\rarr m\in\Omicron(n^2)$

Ritka gráfokat $m\in\Omicron(n)$ függéssel jellemezzük
Sűrű gráfokat $m\in\Theta(n^2)$-el
### Szomszédossági mátrix
Alapesetben $n^2$ bit
Csak az alsóháromszög mátrixot tárolna $n*(n-1)/2$ bit

Mivel $n*(n-1)/2\in\Theta(n^2)$
$$
\Theta(n^2)
$$
### Szomszédossági listás
A listáknak irányítatlan esetben $2m$, irányított esetben $m$ elemük van
$$
\Theta(n+m)
$$

Ritka gráfok esetében $\Theta(n)$
Sűrű gráfok esetében $\Theta(n^2)$
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxMjE2MDg5MF19
-->