# Élsúlyozott gráfok
$G=(V,E)$ rendezett páros, ahol $V$ a csúcsok tetszőleges véges halmaza, $E\subseteq V\times V\backslash\{(u,u):u\in V\}$ (párhuzamos és hurokélek kizárása) pedig az élek, továbbá adott a $w:E\rarr\R$ súlyfüggvény
A $w:E\rarr\R$ minden egyes élhez hozzárendeli annak súlyát, más néven hosszát, illetve költségét(élsúly=élhossz=élköltség)

Élsúlyozott gráfban tetszőleges út költsége az út mentén található élek összsúlya. Hasonlóképpen tetszőleges gráf/fa súlya az élei súlyainak összege
## Gráfábrázolás
$G=(V,E), V=\{1,..,n\},n=\vert V\vert, 1..n,w:E\rarr\R$ 
A gráf egyértelműen azonosítható csúcsai
### Grafikus
#### Irányítatlan
$a-b;n$ azt jelzi, hogy létezik $a$ és $b$ között vonal, közvetlen kapcsolatban vannak egymással és az út költsége $n\in\N$

$a-b,n_1;c,n_2$ a rövidítése $a-b,n_1;a-c,n_2$-nek és az utak költsége $n_1,n_2\in\N$
#### Irányított
$1\rarr2,n$
$1\rarr2,n_1;3,n_2$
### Szöveges
#### Irányítatlan
$u-v_{u_1},w_{u_1};...;v_{u_k},w_{u_k}$ azt jelenti, hogy az $u$ csúcsnak szomszédai a $v_{u_1},...,v_{u_k}$ csúcsok, azaz $(u,v_{u_1}),...,(u,v_{u_k})$ élei a gráfnak, sorban $w(u,v_{u_1})=w_{u_1},...,w(u,v_{u_k})=w_{u_k}$ súlyokkal
#### Irányított
$u\rarr v_{u_1},w_{u_1};...;v_{u_k},w_{u_k}$ azt jelenti, hogy a gráfban az $u$ csúcsból az $(u,v_{u_1}),...,(u,v_{u_k})$ irányított élek indulnak ki, sorban $w(u,v_{u_1})=w_{u_1},...,w(u,v_{u_k})=w_{u_k}$ súlyokkal
### Csúcsmátrixos reprezentáció
$G=(V,E)$ gráfot egy $A/1:\R_\infty[n,n]$ mátrix reprezentálja, ahol $n=\vert V\vert$ a csúcsok száma, $1..n$ a csúcsok sorszámai

$A[i,j]=w(=v_i,v_j)\Rarr (v_i,v_j)\in E$
$A[i,j]=\infty\Rarr (v_i,v_j)\notin E\land i\ne j$

$A[i,i]=0$, hurokél

#### Irányítatlan
| $A$ | $1$ | $2$ | 
|--|--|--|
| $1$ | $0$ | $5$ |
| $2$ | $5$ | $0$ |
Alapján $1$ és $2$ között van vonal és az út költsége $5$

Tárigény csökkentése érdekében elég egy alsó- vagy felsőháromszög mátrixot felrajzolni, ugyanis oda-vissza irányról nem beszélünk

$B:\R_\infty[n(n-1)/2]$
$A[i,j]=B[(i-1)(i-2)/2+(j-1)]$, ha $i\gt j$ - alsóháromszög mátrix
$A[i,j]=A[j,i]$, ha $i\lt j$ - felsőháromszög mátrix
#### Irányított
| $A$ | $1$ | $2$ | 
|--|--|--|
| $1$ | $0$ | $5$ |
| $2$ | $\infty$ | $0$ |
Alapján $1$-ből mutat $2$-be egy vonal és az út költsége $5$
### Szomszédossági listás
$A/1:Edge*[n]$ pointertömb segítségével ábrázoljuk ami 
* `v` $(v\in\N)$
* 'w' $(w\in\R)$
* `next` (Edge pointer)
#### Irányítatlan
A pointertömb $i$-edik eleme tartalmazza az $i$ edik csúcs szomszédait
Egy kapcsolatot a tömb mind a két elemében jeleznünk kell
#### Irányított
A pointertömb $i$-edik eleme tartalmazza az $i$ edik csúcs gyerekeit

$A[1]->v=3;A[1]->next->v=4;A[1]->next->next->0$
$A[4]$
Jezi azt a gráfot ahol $1$ mutat $3$-ba és $4$-be, és $4$ nem mutat semmibe
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ0ODQ3MDgyNF19
-->