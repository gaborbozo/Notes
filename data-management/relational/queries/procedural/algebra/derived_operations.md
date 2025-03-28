# Műveletek
## Metszet (Intersection)
Két kapcsolat közös rekordjait tartalmazza
$$
\cap
$$
## Csoportosítás (GroupBy)
A kapcsolatot csoportokra osztja az egyes csoportokat meghatározó mezők szerint
$$
\Gamma
$$
# Összekapcsolások
## Theta-összekapcsolás (Theta Join) és egyen-összekapcsolás (Equi join)
$r,s$ sémában $R(A_1,...,A_n),S(B_1,...,B_n)$ nincs közös attribútum.
$$
\begin{array}{c}R\bowtie S\\A_i=B_j\end{array}=\begin{array}{c}r\vert x\vert s\\A_i\Theta B_j \end{array}=\sigma_{A_i\Theta B_j}(r\times s)
$$
```sql
SELECT * FROM R,S WHERE R.common_field = S.common_field;
```
> $A_i=B_j$ feltétel esetén egyen-összekapcsolás.
## Természetes-összekapcsolás (Natural Join)
$r,s$ sémái $R(A_1,..,A_n,B_1,...,B_k),S(B_1,...,B_k,C_1,...,C_m)$
$$
R\bowtie S
$$
```sql
SELECT * FROM R NATURAL JOIN S;

SELECT DISTINCT A,R.B,C FROM r,s WHERE R.B=S.B
```
## Félig-összekapcsolás (Semi join)
$$
\ltimes,\rtimes
$$
## Ellentétes összekapcsolás (Antijoin)
$$
\triangleright
$$
## Osztás (Division)
$$
\%
$$
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzkwNzMyNjkzXX0=
-->