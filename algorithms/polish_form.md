# Lengyel forma
```
infix: (A+B)*C-D
Prefix: -*+ABCD
Postfix: AB+C*D-
```

## Precedencia

## Operátorok közötti esetek

* **Veremben gyengébb**: Betesszük a beolvasott operátort a verembe
* **Veremben erősebb**: Kivesszük a verem tetejéről az operátort és a beolvasottat betesszük a helyére
* **Azonos erősségű**: Kivesszük és betesszük a helyére
Az utóbbi eset csak "balról jobbra sorrend" esetén alkalmazható. 
Ellenpélda a hatványozás. Ebben az esetben nem veszünk ki semmit csak akkor ha a következő operátor alacsonyabb precedenciájú, de akkor az az összes ilyen "jobbról balra sorrendű" opetárort 
## Ábrázolás és kiértékelés
### LIFO adattípus
Az operandusok kerülnek be az adatszerkezetbe
Beolvasott operátor esetén kiveszünk kettőt és végrehajtjuk rá a műveletet
### Bináris fa
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTI1NDYwNzUxXX0=
-->