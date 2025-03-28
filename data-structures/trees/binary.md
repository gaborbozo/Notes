# Bináris fák
## Ábrázolás
### Két pointeres
`left,right` attribútum
### Három pointeres
`left,right,parent`  attribútum

---
Egy bináris fa nulladik szintje a fa csúcsa
Hierarchikusan lesznek gyerekeből szülők
A fa legalsó szintjén lévő gyerekeket levélnek nevezzük 
## Definíciók
* **Szigorúan bináris fa**, ha a fa minden belső pontjának két gyereke van
* **Teljes bináris fa**, ha olyan szigorúan bináris fa, ahol minden levél azonos szinten helyezkedik el
* **Majdnem teljes bináris fa**, ha olyan teljes bináris fa, melynek legalsó (levél) szintjéről elhagytunk néhány levelet (de nem az összeset)
* **Majdnem teljes, balra tömörített bináris fa**, ha majdnem teljes bináris fa, de levelek a legalsó szinten csak jobb oldalról hiányozhatnak. Ezeket **szintfolytonos fáknak** is nevezzük
## Szintfolytonos elhelyezkedés
Bináris fák aritmetikai ábrázolása

Következménye, hogy a fában való navigálás a tömb indexeinek segítségével történik
Ha az indexeket $1$-től számozzuk
* csúcs indexe $i$
* bal gyerekének indexe $i*2+1$
* jobb gyerekének indexe $i*2+2$
* szülő indexe $\frac{i}{2}-1$
Ha az **indexelés egytől** kezdődik, akkor bal: $i*2$, jobb: $i*2+1$, szülő $\frac{i}{2}$ alsó egészrész
## Fák bejárása
### Preorder
1. levél kulcsa
2. bal levele
3. jobb levele
### Inorder
1. bal levele
2. levél kulcsa
3. jobb levele
### Postorder
1. bal levele
2. jobb levele
3. levél kulcsa
### Szintfolytonos/Szélességi
A bináris fa csúcsait a mélységük szerinti sorrendben látogatjuk meg, egy szinten belül balról jobbra
FIFO adattípus alkalmazása

## Fák építése
### Két bejárást alkalmazva
*  Preorder + Inorder
* Postorder + Inorder

Preorder + Postorder nem létezik, mert egy-gyerekes csúcsnál nem lehet eldönteni, hogy az egy-gyerek melyik irányban van
## Bináris fák zárójelezett, szöveges formája
( balRészFa gyökér jobbRészFa )
# Bináris keresőfák
Tetszőleges csúcs kulcsánál a bal részfájában minden csúcs kulcsa kisebb, a jobb részfájában minden csúcs kulcsa nagyobb.
Egyenlőségről csak **rendezőfa** esetében beszélünk
## Alapműveletek
* `search(t,k)`
* `insert(t,k)`
* `remMin(t,minp)` - Fából törli a minimumot és a `minp` címkébe másolja 
* `remove(t,k)`
## Fák építése
### Bejárást alkalmazva
*  Preorder
* Postorder
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNDk0MTMxMzZdfQ==
-->