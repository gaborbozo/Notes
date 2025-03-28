# Hasító táblák
A hasító táblák célja egy olyan adattárolási eljárás megvalósítása, amelyben a keresés, beszúrás és törlés (szótár)-műveletek várhatóan nagyon hatékonyak
Ezen túl a nyílt címzés feloldja az $U>>n$ problémát, miszerint nagy indexű adatok címzéséhez nem feltétlen kell azonosan nagy mennyiségű hely allokálása
## Direkt címzés
Ha a kulcshalmaz nem túl nagy
$U=[0..m)$, hogy egy $m$ méretű tömbben, hasítóblában tárolhatjuk a rekordokra mutató pointereket úgy, hogy a tömb $k$ indexű tagja a $k$ kulcsú rekordra mutat
## Láncolt hashelés
$m$ darab `S1L` listában tároljuk az adatrekordokat
A hasítótábla $T[i]$ eleme az $i$ láncolt lista első elemére mutató pointer
Ez a lista azokat a $k$ kulcsú elemeket tartalmazza, amikre $h(k)=i$
Beszúráskor a megfelelő lista elejére szúrjuk be az új elemet
Duplikált kulcsok ellenőrzése
## Nyílt címzés
$m$-darab hasítófüggvény
Ebben az esetben az adatrekordokat a hasítótábla réseiben tároljuk
Kulcsütközés áthidalására a próbafüggvény nyújt segítséget, aminek lényege, hogy egy már elfoglalt index esetén új indexet válasszon valamilyen függvény segítségével
$h:U\times0..(m-1)\rarr0..(m-1)$ - próbafüggvény
$\lang h(k,0),h(k,1),..,h(k,m-1)\rang$ - potencionális próbasorozat
Műveletektől függően általában addig ismételjük a próbafüggvényt, amíg meg nem találtuk a keresett elemet/üres mezőt/ki nem merítettük a próbasorozatot
### Lineáris próba
Számtani sorozatot alkot, differenciája leggyakrabban $+1/-1$

$h(k,i)=(h_1(k)+i)\mod m$ $i=0,1...,m-1$

**Elsődleges csomósodást** tapasztalhatunk kulcsütközés esetén az azonos próbasorozatok miatt könnyen besűrüsödhet a tábla
### Négyzetes próba
$h(k, i)=(h_1(k)+c1*i+c2*i2)\mod m$ 
$i=0,1,..m-1,c_2\ne0$
$c_1,c_2$ konstansokat úgy kell megválasztani, hogy a próbasorozat teljes táblát kiadja

Abban az esetben ha $m$ egy kettőhatvány, akkor $c_1=c_2=\frac{1}{2}$ megfelelő választás
Ilyenkor a képlet is leegyszerüsödik: $h(k,i)=(h(k,i-1)+i)\mod m$
$i=1,2,...m-1$ 

**Másodlagos csomósodás** tapasztalhatunk, ugyanis az azonos próbasorozatok mentén hasonlóan sűrüsödnek az elemek
### Kettős hasítás
Ebben az esetben a próbasorozat hasonlóan egy számtani sorozat, viszont a differencia kulcsonként eltérő
$h_1:U\rarr0..m-1$
$h_2:U\rarr1..(m-1)$

$h(k,i)=(h_1(k)+i*h_2(k))\mod m$
$i=0,1..,m-1$

* $h_2$ semmilyen $k$ értékre nem adhat nullát
* Tetszőleges $k$ érték esetén relatív prím a tábla méretéhez képest
Általában a tábla mérete prím, így ez nem is probléma
## Hasítófüggvény megválasztása
$h:U\rarr0..(m-1)$ függvény egyszerű egyenletes hasítás, ha a kulcsokat a rések között egyenletesen szórja szét, azaz hozzávetőleg ugyanannyi kulcsot képez le az $m$ rés mindegyikére
### Osztó módszer
Ha a kulcsok egész számok, gyakran 
$$
h(k)=k\mod m
$$
Ha $m$ olyan prím, amely nincs közel a kettő hatványokhoz, akkor általában egyenletesen szórja szét a kulcsokat $0..(m-1)$ intervallumon
pl $2000$ rekord $\alpha=3$ kitöltöttségi aránnyal: $2000/3=700\Rarr701$ jó választás
$512<701<1024$ - egyikhez sincsen közel
### Kulcsok a [0,1) intervallumon
Ha egyenletesen oszlanak el, a 
$$
h(k)=[k*m]
$$ függvény is kielégíti az egyszerű, egyenletes hasítás feltételét
### Szorzó módszer
Az osztó módszerrel ellentétben itt a tábla mérete lehet bármi
Ha a kulcsok valós számok, tetszőleges $0\lt A\lt1$ konstanssal alkalmazható a 
$$
h(k)=[\{k*A\}*m]
$$ hasító függvény($\{x\}$ törtrész)
$A=\frac{\sqrt{5}-1}{2}$ választással egész jó eredményeket kaphatunk
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTY1MjQ4MzU1XX0=
-->