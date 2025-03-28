# Általános fák
Az általános fák esetében a bináris fákkal összehasonlítva, egy csúcsnak tetszőlegesen sok gyereke lehet
Itt azonban tetszőleges csúcshoz tartozó részfák száma pontosan egyenlő a gyerekek számával, azaz nem tartoznak hozzá üres részfák (legfeljebb egy csúcsú részfákról, azaz egy részfának csak a gyökeréről beszélhetünk)

Ha a gyerekek sorrendje lényeges, akkor rendezett fákról beszélünk

Modellezhetjük velük a számítógép mappáinak hierarchiáját, programok blokkstruktúráját, függvénykifejezéseket
## Ábrázolás
Bináris láncolt reprezentáció
* `child`
* `sibling`
* `key`

`p` csúcs levél, ha `child=0`
`p` csúcs utolsó testvér, ha `sibling=0`
## Jelölés
A gyökeret előre szokás venni, így egy nemüres fa általános alakja
$$
(G\ t_1...t_n)\text{ ahol }G\text{ a gyökércsúcs tartalma }t1...tn\text{ pedig a részfák}
$$
pl `{ 1 [ 2 (5) ] (3) [ 4 (6) (7) ] }`
* $1$ a gyökér csúcs
* $1$-nek a gyerekei a $2,3,4$
* részfák a $2\ (5)$, $3$, $4\ (6)\ (7)$
* a fa levelei $5,3,6,7$
## Fák bejárása
Preorder bejárása a `child - left` és `sibling - right` megfeleltetéssel

Bináris reprezentáció preorder bejárást igényel

A postorder bejáráshoz azonban a bináris reprezentáció inorder bejárása szükséges
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzk2MDQ5ODYwXX0=
-->