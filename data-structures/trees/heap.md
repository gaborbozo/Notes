# Kupac
* **Maximum kupac** egy majdnem teljes, balra tömörített bináris fa, melynek minden belső pontjára teljesül, hogy a belső pont kulcsa nagyobb vagy
egyenlő a gyerekei kulcsánál
Így kupac tetején (a fa gyökerében) mindig az egyik legnagyobb
elem található
* **Minimum kupac**  a szülő kulcs kisebb vagy egyenlő a
gyerekei kulcsánál.
## Műveletek
* `insert` Beszúrja a tömb utolsó eleme után, majd addig emeli a fában, amíg helyreáll a kulcsokra vonatkozó feltétel (szülő nagyobb vagy egyenlő mind a kettő elemnél)
* `deleteMax` A legnagyobb kulcs helyére a fa legalsó szintjének legjobboldalibb levele kerül(hogy megmaradjon a balra tömörítettség). Ezután addig süllyed amíg a kulcsokra vonatkozó feltétel helyre nem áll
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExNjA2ODAwN119
-->