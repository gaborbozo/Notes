```mermaid
graph TB
i0(alkalmazás)
i1(elem)
i2(átalakítás)
i3(algebrai optimalizáció, szabályok alkalmazása)
i4(várható méretek becslése)
i5(fizikai tervek készítése)
i6(költségek becslése)
i7(a legjobb kiválasztása)
i8(végrehajtás)

i0 -- sql lekérdezés --> i1 -- elemző fa ---> i2 -- logikai lekérdező terv --> i3 -- javított logikai lekérdező terv --> i4 -- logikai lekérdező és méretek --> i5 -- FT1,FT2,... --> i6  -- FT1-K1, FT2-K2 --> i7 -- FTi --> i8 -- eredmény --> i0 
```
## Elemzőfa (Parse tree)

* **Statikus adatbázis** amely ritkán módosul, a lekérdezések gyorsasága a fontosabb.
* **Dinamikus adatbázis** amely gyakran módosul, ritkán végünk lekérdezést.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MzMyMjY0OTRdfQ==
-->