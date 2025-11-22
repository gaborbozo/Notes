# Függvények aszimptotikus viselkedése
**Aszimpotitkusan pozitív** egy függvény, ha
$$
\exist N\in\N,\forall n\gt N:f(n)\gt0
$$
## $f$-nek $g$ aszimptotikus felső korlátja $\Big(f(n)=\Omicron\big(g(n)\big)\Big)$
$f$ legfeljebb olyan gyorsan nő, mint $g$
$f\prec g\Lrarr f\in\Omicron(g)$
$$
\Omicron(g)=\{f\vert\exist c\gt0\land N\in\N,\forall n\ge N:f(n)\le c\cdot g(n)\}
$$
## $f$-nek $g$ aszimptotikus alsó korlátja $\Big(f(n)=\Omega\big(g(n)\big)\Big)$
$g$ legfeljebb olyan gyorsan nő, mint $f$
$g\prec f\Lrarr f\in\Omega(g)$
$$
\Omega(g)=\{f\vert\exist c\gt0\land N\in\N,\forall n\ge N:c\cdot g(n)\le f(n)\}
$$
## $f$-nek $g$ aszimptotikus éles korlátja $\Big(f(n)=\Theta\big(g(n)\big)\Big)$
$$
\Theta(g)=\{f\vert\exist c_1,c_2\gt0\land N\in\N,\forall n\ge N:c_1\cdot g(n)\le f(n)\le c_2\cdot g(n)\}
$$
## Aszimptotikusan kisebb és nagyobb függvény
$f,g:\N\rarr\R$ 
* **Aszimptotikusan kisebb** $f$ függvény, mint $g$
$f\prec g\Lrarr\lim\limits_{n\rarr\infty}\frac{f(n)}{g(n)}=0$
* **Aszimptotikusan nagyobb** $f$ függvény, mint $g$, ha $g\prec f$
# Függvények aszimptotikus nagyságrendje
$\Omicron,\Omega,\Theta$ $2$-aritású relációnak is tekinthető az $\N\rarr\R_0^+$ függvények univerzumán, ekkor
* $\Omicron,\Omega,\Theta$ tranzitív
  > Például $f=\Omicron(g)\land g=\Omicron(h)\Rarr f=\Omicron(h)$
* $\Omicron,\Omega,\Theta$ reflexívek
* $\Theta$ szimmetrikus
* $\Omicron,\Omega$ fordítottan szimmetrikus
  > $f=\Omicron(g)\Lrarr g=\Omega(f)$
## Következmény, ekvivalenciareláció
$\Theta$ ekvivalenciareláció az $\N\rarr\R_0^+$ függvények egy osztályozását adja.

Általában ezeket az osztályokat a legegyszerűbb tagjukkal reprezentáljuk.
> Például korlátos függvények, lineáris függvények, négyzetes függvények stb.
## Műveletekre vonatkozó tulajdonságok
* $f,g=\Omicron|\Omega|\Theta(h)\Rarr f+g=\Omicron|\Omega|\Theta (h)$ 
* $c\gt0,f=\Omicron|\Omega|\Theta(g)\Rarr c\cdot f=\Omicron|\Omega|\Theta(g)$
* $f+g=\Theta(\max\{f,g\})$ (**szekvencia tétele**)
  > A domináns tag határozza meg egy összeg aszimptotikus nagyságrendjét. 
* Ha létezik az $f/g$ határérték
  * ha $f(n)/g(n)\rarr+\infty\Rarr f(n)=\Omega(g(n))\land f(n)\ne\Omicron(g(n))$
  * ha $f(n)/g(n)\rarr c\ (c\gt0)\Rarr f(n)=\Omicron(g(n))$
  * ha $f(n)/g(n)\rarr0\Rarr f(n)=\Omicron(g(n))\land f(n)\ne\Omega(g(n))$
## Konkrét függvények
* $\forall p(n)=a_kn^k+...+a_1n+a_0\ (a_k\gt0)$-ra $p(n)=\Theta(n^k)$
* $\forall p(n)$ polinomra és $c\gt1$ konstansra $p(n)=\Omicron(c^n)$, de $p(n)\ne\Omega(c^n)$
* $\forall c\gt d\gt1$ konstansokra $d^n=\Omicron(c^n)$, de $d^n\ne\Omega(c^n)$
* $\forall a,b\gt1$-re $\log_an=\Theta(\log_bn)$
* $\forall c\gt0$-ra $\log_2n=\Omicron(n^c)$, de $\log_2n\ne\Omega(n^c)$
# Nagyságrendek
1. $\Theta(1)$ pl. Verem művelet
2. $\Theta(\log n)$ pl. Bináris keresés
3. $\Theta(\sqrt n)$ pl. Prímszámteszt
4. $\Theta(n)$ pl. Lineáris keresés
5. $\Theta(n\log n)$ pl. Összefésülő rendezés
6. $\Theta(n^2)$ pl. Beszúrórendezés
7. $\Theta(n^3)$ pl. Mátrixszorzás
8. $\Theta(2^n)$ pl. Hanoi tornyai
9. $\Theta(n!)$ pl. Utazóügynök-probléma
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NjQ1MTU2NzldfQ==
-->