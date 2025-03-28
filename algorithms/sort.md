# Rendezések és tulajdonságaik
## Lineáris idejű rendezések
### Radix
Rendezés láncolt listákra
$r$ alapú számrendszerben felírt, $d$ számjegyű, előjel nélküli egész számok
$i:=d..1$-szor végig megy az $i$-edik helyiértékeken és valamilyen **stabil**, feltehetőleg lineáris idejű rendezés használata (**általában leszámoló rendezés**) 
### Distributing
A radix egy általánosítottab verziója, ahol is egy $\varphi$ kulcsfüggvény a megfelelő helyiértékű számjegyet választja ki az iteráció során
### Counting
Radix rendezés ideális segédrendezése tömbökre kivetítve
### Bucket
$[0,1)$ kulcsú számok rendezésére
A tizedesjegyet megvizsgálva listákba pakoljuk a számokat, majd az egyes listákat belső rendezés után megfelelő sorrendben összefűzzük

---
Egy rendező eljárást **stabilnak** nevezünk, ha az algoritmus nem változtatja meg az egyenlő kulcsú elemek egymáshoz viszonyított sorrendjét.

| Algorithm | Best | Average | Worst |
|--|--|--|--|
| Merge Sort | $\varOmega(n\log(n))$ | $\Theta(n\log(n))$ | $\Omicron(n\log(n))$ |
| Heap Sort | $\varOmega(n\log(n))$ | $\Theta(n\log(n))$ | $\Omicron(n\log(n))$ |
| Insertion Sort | $\varOmega(n)$ | $\Theta(n^2)$ | $\Omicron(n^2)$ |
| Quick Sort | $\varOmega(n\log(n))$ | $\Theta(n\log(n))$ | $\Omicron(n^2)$ |
| Selection Sort | $\varOmega(n^2)$ | $\Theta(n^2)$ | $\Omicron(n^2)$ |
| Bubble Sort | $\varOmega(n)$ | $\Theta(n^2)$ | $\Omicron(n^2)$ |
| Radix Sort | $\varOmega(nk)$ | $\Theta(nk)$ | $\Omicron(nk)$ |
| Counting Sort | $\varOmega(n+k)$ | $\Theta(n+k)$ | $\Omicron(n+k)$ |
| Bucket Sort | $\varOmega(n+k)$ | $\Theta(n+k)$ | $\Omicron(n^2)$ |
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY2NjI1MDU3XX0=
-->