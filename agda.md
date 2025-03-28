# Agda
# Important hotkeys
`C-c C-l` - Typecheck
`C-c C-r/C-c C-r` - Create hole
`C-c C-n` - Normalize expression
`C-c C-d` - Infer expression
`C-c C-,` - Check goal context
`C-c C-.` - Compare goal and code
`C-c C-SPC` - Take out hole and fill with correct code
`C-c C-c [variable name]`  - case split with additional variable name
`C-c C-a` - auto solution in some case
`C-u C-u C-c C-,` - goal and context

$\N$ - `\bN`
$\rarr$ - `\r`
$\lambda$ - `\Gl`
# Logical connectivities
| Statement | Type |
|--|--|
| $A\land B$ | $A\times B$ |
| $A\lor B$ | $A⊎B$ |
| $A\Rarr B$ |$A\rarr B$ |
| $true$|$\top$ |
| $false$ | $\bot$ |
| $\lnot A$ | $A\rarr\bot$ |
| $\Lrarr$ | $(P\Rarr Q)\land(P\Rarr Q)$ |
$A\land B$ Bizonyítjuk $A$-t és $B$-t, ennek megfeleltetése az $A\times B$
$A\lor B$ Valamelyiket a kettő közül be kell bizonyítani
$A\Rarr B$-ből való bizonyításhoz kell írni egy programot ami $A$-ból $B$-be képez
$\top$ Azonosan igaz állítás, hasonló mint a $true$
$\bot$ Azonosan hamis állítás, aminek fixen nincs eleme, hasonló mint a $false$. Alapvetően úgy definiáltuk, hogy nincs eleme és baj lenne ha kiderülne, hogy mégis van
$\lnot A$ bizonyításához kell egy program ami $A$-ból semmit csinál
# Definitions
## Function
In Type Theory functions are a fundamental concept - We need functions to say what a relation is
Namely a relation between $A$ and $B$ is a function from $A$ and $B$ to the type of propositions
##  Binding and authority
$(\lambda\ x\rarr x+3)\ 2=(x + 3)[x\rarr2]$
Az összes szabad $x$-et $x+3$ kifejezésben kötöm $2$-vel
## Hideing
$((λ\ x → (λ\ x → x)) 2) 3 =((λ x → (λ x → x)))$
## Variable capture
```haskell
(λ x -> (λ y -> x + y)) y
-> λ y -> y + y
```
Wrong because $y$ refers to the bound variable $y$ and not to our top-level $y$. It has to be avoided and alpa equiavelnce solves it
## Alpha equivalence
The principle that two syntactic expressions are equivalent for all purposes if their only difference is the renaming of bound variables
```haskell
λ y -> x + y = λ z -> x + z
```
## Beta reduction
Replacing the parameter with the argument

$(\lambda\ x\rarr t)t'=t[x\rarr t']$
$(\lambda\ n\rarr n*n)5=5*5$

The two term aside `=` are beta equal with eachother
## Partial application
The process of fixing a number of arguments to a function, producing another function of smaller arity
## Alpha abstraction
A way of defining a function without its name
```haskell
add : Nat -> (Nat -> Nat)
add = λ x -> (λ y -> x + y)
```
## Eta($\eta$)-equality
Two functins which are equal when applied to the same argument should be considered equal
```haskell
M = λ x -> M x
  = λ x -> N x
  = N
```
## -----
$f(a,b,c)\rarr f(a)(b)(c)$ 
## Right association
`Nat -> (Nat -> Nat)` equals with `Nat -> Nat -> Nat`
# Functions
## Higher order functions
Instead of returning a function we can also have functions that have functions as input

```haskell
k : (Nat -> Nat) -> Nat
k h = h 2 + h 3

k add2 = add2 2 + add2 3
		= (2 + 2) + (3 + 2)
		= 9
```
## Polymorphic functions
Functions work for any type
```haskell
--id function works for every Set
--Agda automatically instantiate A
id : {A : Set} -> A -> A
id x = x
```
### Variable
```haskell
A : Set
id : A -> A
```
## Infix function
```haskell
-- _ means an argument
-- The price we have to pay for this flexibility is that we have to separate any syntactical component with spaces
_∘_ : (B -> C) -> (A -> B) -> (A -> C)
(f ∘ g) x = f (g x)
```
# Data
```agda
data Nat : Set where
    zero : Nat
    suc  : Nat → Nat
```
## Maybe
```haskell
data Maybe (A : Set) : Set where
	nothing : Maybe A
	just : A -> Maybe A

```
## Record
```haskell
record Person : Set where
	field
	id : Nat
	phone : Nat

-- open Person //namespace
-- id bill = 12

Person.id bill = 12
Person.phone bill = 6322643


record _x_(A B : Set) : Set where
	constructor _,_
	field
		fst : A --proj1
		snd : B --proj2
		
```
# Basic type formers
## disjoint union
Either $A$ or $B$ - Diszjunkt unió
Vagy az egyik vagy a másik
```haskell
data _⊎_ (A B : Set) : Set where
	injl : A -> A ⊎ B
	injr : B -> A ⊎ B
```
Insensitive to the representation of any type
$2\uplus3=\{inj1,zero2;inj1,one2;inj2,zero3;inj2,one3;inj2,two3\}$

```haskell
data Colour : Set where
	red green blue pink : Colour

colToℕ : Colour → ℕ
colToℕ  red = 1
colToℕ  green = 2
colToℕ  blue = 3

retnum : ℕ  ⊎  Colour → Maybe  Colour
retnum (inj1 n) = nothing
retnum (inj2 c) = just c
```
## Product
```haskell
record _x_ (A B : Set) : Set where
	
	constructor _,_ -- Pairing constructor automatically added
	-- _,_ : A -> B -> A x B
	-- proj1 (a , b) = a
	-- proj2 (a , b) = b
	field 
		proj1 : A x B -> A
		proj2 : A x B -> B
```
We can construct elements of `A x B` by specifying what the result is when applying projections. This is called **copatternmatching**
$A=\{2\times 3=\{zero2,zero3;zero2,one3;zero2,two3;one2,zero3;one2,one3;one2,two3\}$
```agda
curry : (A x B -> C) -> (A -> B -> C)
curry f = λ a b -> f (a , b)

uncurry : (A -> B -> C) -> (A X B -> C)
uncurry g = λx -> λ (proj1 x) (proj2 x)

curry (uncurry g) = g
```
## Strong case
```haskell
case-c : (A -> C) x (B -> C) -> A ⊎ B -> C
case-c = uncurry case x = {!!}
```
## The unit type/nullary product
 an empty record
```haskell
record  ⊤ : Set  where
tt : ⊤
tt = record {}
```
  

## The empty type/empty product
an empty data with no fields
an empty data
```haskell
data  ⊥ : Set  where
```
## exfalso
kap egy ⊥ és abból csinál bármit
Be van égetve, hogy ha az üres típusnak egy elemét előállítod, akkor bármit tudsz csinálni
Azonos a hamis állítással
Indirekt bizonyításokhoz
```haskell
case : ∀{i}{A : Set i} -> ⊥ -> A
exfalso()
```
## Case
```haskell
case : ∀{i j k}{A : Set}{B : set j}{C : Set k}
	(t : A ⊎ B)(u : A -> C)(v : B -> C) -> C
case (inl t) u v = u t
case (inr t) u v = v t
```
## Refl
Ha ki tudja következtetni a két egyenlőség jelet, akkor meghívja a `refl` konstruktort
```haskell
infix 4 ≡
data _≡_ {A : Set a} (x : A) : A -> Set a where
	instance refl : x = x


1issuczero : 1 ≡ suc zero
1issuczero = refl
```
# Recursion
```
double : Nat -> Nat
double zero = zero
double (suc n) = suc(suc(double n))

double 3 = double(suc(suc(suc zero))) 
         = suc(suc(double(suc(suc zero)))) 	
         = suc(suc(suc(suc(double(suc zero)))))
	     = suc(suc(suc(suc(suc(suc(double zero)))))) 
	     =suc(suc(suc(suc(suc(suc zero))))) = 6
```
## Iterator and Recursor
# Arithmetic operations
## Addition
```
_+_ : Nat -> Nat -> Nat
zero + n = n
suc m + n = suc (m + n)
```
## Multiplication
```
_*_ : Nat -> Nat -> Nat
zero * n = 0
suc m * n = n + m * n
```
## Exponential
```
_^_ : Nat -> Nat -> Nat
m ^ zero = 1
m ^ suc n = m * m ^ n
```
## Ackerman
# Datatypes
## Simple
## Parametrized
## Indexed
## Inductive
Of an inductive datatype which we can view as a recursively defined sum
### List
```haskell
data List (A : Set) : Set where
	[] : List A
	_::_ : A -> List A -> List A

length : List A -> N
length [] = 0
length (x :: l) = 1 + length l

_++_ : List A -> List A -> List A
[] ++ ys = ys
(x :: xs) ++ ys = x :: (xs ++ ys)

map : (A ! B) ! List A ! List B map f [] = [] 
map f (x :: xs) = f x :: map f xs
```
### Syntax tree
```haskell
data Expr : Set where
	const : N -> Expr
	_[+]_ : Expr -> Expr -> Expr
	_[*]_ : Expr -> Expr -> Expr

{-
2 * (3 + 4)

 *
/  \
2   +
   / \
   3 4
-}

eval : Expr -> Nat
eval (const  x) = x
eval (e1  [+]  e2) = eval  e1  *  eval  e2
eval (e1  [*]  e2) = eval  e1  +  eval  e2

height : Expr -> Nat
height (const  x) = zero
height (_ [+]  expr) = 1  +  height  expr
height (_ [*]  expr) = 1  +  height  expr
```
### Tree
```haskell
data  Tree (A : Set) : Set  where
	leaf : Tree  A
	node : Tree  A → A → Tree  A → Tree  A

t = node (node  leaf  1 (node  leaf  2  leaf)) 5  leaf
{-
    5
   / \
  1
 / \
    2
   / \
-}

tree2List : {A : Set} -> Tree A -> List A
tree2List  leaf = []
tree2List (node  t1  k  t2) = tree2List  t1  ++ (k  ∷  tree2List  t2)

list2tree : List  ℕ → Tree  N
list2tree  [] = leaf
list2tree (a  ∷  as) = insert  a (list2tree  as)

insert : ℕ → Tree  ℕ → Tree  ℕ
insert k leaf = node leaf k leaf
insert k (node t1 l t2) = if (k ≤ l) then (node (insert k t1) l t2) else (node t1 l (insert k t2))
```
### Rose tree
```haskell
data RoseTree : Set where
	node : List RoseTree -> RoseTree
``` 
### Ordinals
Infinitely branching trees and a nice application of those is a notation for ordinal numbers
```haskell
data Ord : Set where
	zero : Ord
	suc : Ord ! Ord
	lim : (N ! Ord) ! Ord
```
## Coinductive
An example of a coinductive type is the type of streams, or infinite sequences. Given a stream over $A$ we can obtain its head which is an element of $A$ and its tail which is another stream
### Streams
```haskell
record Stream (A : Set) : Set where
	constructor _::_
-- _::_ : A ! Stream A ! Stream A
-- head (a :: as) = a
-- tail (a :: as) = as
	coinductive 
	field
		head : A 
		tail : Stream A
```
### Conatural
### Coiterator and corecursor
## Dependent
```haskell
-- depends by b
A : B -> Type
```
```haskell
data  Vec (A : Type) : ℕ → Type  where
	[] : Vec  A  0
	_∷_ : {n : ℕ} → A → Vec  A  n → Vec  A (suc  n)

Vec Nat : Nat -> Type
Vec Nat 0 : Type --0 hosszú vektor típusa

zerolengthvector : Vec Nat 0
zerolengthvector = []

twolengthvector : Vec Nat 2
twolengthvector = 3 :: 2 :: []
```
called dependent type because a term appears in an additional type
final result depends on the type of the function

Another example for dependent types are polymorhpic types
```haskell
(A B : Type) -> A x B <-> B x A
```
Dependent functions are types with output values were given as an input - input apperas in the output
```haskell
zeroes-v : (n : Nat) -> Vec Nat n
```
### Fin
Using dependent types we can avoid run-time errors such as the typical index out of range error we get when accessing an array
Fin provides us with the allowed index-range of a vector
```haskell
data Fin : ℕ → Set where
	zero : {n : ℕ} → Fin (suc n)
	suc : {n : ℕ} → Fin n → Fin (suc n)

Fin 0 = {} 
Fin 1 = {zero {0}} 
Fin 2 = {zero {1},suc {1} (zero {0})} 
Fin 3 = {zero {2},suc {2} (zero {1}),suc {2} (suc {1} (zero {0}))}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NjU5MTcyNl19
-->