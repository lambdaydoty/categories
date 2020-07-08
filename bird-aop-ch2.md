# AoP 2 - Functions and Categories

###### tags: `cat` `fp` `Bird`

> *One does not so much learn category theory as absorb it over a period of time.*
---

[TOC]

---

## 2.1 Categories

### Definition $\mathcal{C}$

1. Noun
    1. *objects*, *dots*: $Obj(C)$, $C_0$
    2. *morphisms*, *arrows*: $Mor(C)$, $C_1$
    3. \`pairs\` of morphisms: $C_2$.
2. Verb
    1. A pair of total operations, $s,t : C_1 \rightrightarrows C_0$
    2. A total operation, $id :C_0 \rightarrow C_1$
    3. A partial operation, $\circ : C_2 \rightarrow C_1$
3. Law
    1. $f \circ g$ is defined for $t\cdot g = s\cdot f$
    2. Associativity for $\circ$
    3. Identity for $\circ$, $id$
4. Commutativity
    * ![](https://i.imgur.com/HPSVtH2.png =150x90)

---

![](https://i.imgur.com/m1DtUzM.png =280x150)

> [Notation]
> We will denote a morphism $f$ with $A = t(f)$ and $B = s(f)$ by $f : A \leftarrow B$ and sometimes more succintly by $f_{AB}$
> 

---

### Examples


1. Shapes
    * **1**, the "object" ![](https://i.imgur.com/2w4J3Yf.png)
    * **1** + **1**, the "pair" ![](https://i.imgur.com/hvhbHOl.png)
    * **2**, the "arrow", ![](https://i.imgur.com/tao3Wrb.png)
    * **I**, the "isomorphism", ![](https://i.imgur.com/Ublvvgx.png)
    * Oridinal categories
2. Preorders
3. Monoids
4. **Fun**/**Set**, **Par**, **Rel**, ...
5. Product of Categories: $\mathcal{C} \times \mathcal{D}$
6. The arrow category: $\text{Arr}(\mathcal{C})$


```mermaid
graph TD
    Partial-order --> Total-order
    
    Magma -- associativity --> Semigroup -- identity --> Monoid -- invertibility --> Group
    
    Category:::someclass --> Preorder
    
    Category --> Monoid
    
    Preorder -- antisymmetry --> Partial-order
    
    classDef someclass fill:#f96;
```

## 2.2 Functors

> A *functor* is a homomorphism between categories
> 

![](https://i.imgur.com/AJpbZ9q.png)

> Functors themsolves forms a category:
> * Functors can be composed as $(F \cdot G)f = F(Gf)$
> * For every category $\mathcal{C}$, there is an identity function $id : \mathcal{C} \leftarrow \mathcal{C}$
> 

### Examples

1. For $\mathcal{C}$, the identity function $id: C \leftarrow C$.
2. For categories $\mathcal{A}, \mathcal{B}$, $A \in Obj(\mathcal{A})$, the *constant functor* $K_A : \mathcal{A} \leftarrow \mathcal{B}$
3. The *product* (bi)functor $(\times) : \text{Fun} \leftarrow \text{Fun} \times \text{Fun}$

![](https://i.imgur.com/Qah5TFk.png)

![](https://i.imgur.com/aW6ummA.png)


## 2.3 Natural Transformations

> *I didn't invent categories to study functors; I invented them to study natural transformations.*
> 

Recall:

0. Objects: $A, B, C, ...$
1. Morphism $f$: Point $B$ $\leadsto$ Point $A$
2. Functor $F$: Line ![](https://i.imgur.com/BywFl4T.png =30x100) $\leadsto$ Line ![](https://i.imgur.com/mg9vgQ1.png =30x100)
3. Natural Transformations: Plain $S$ $\leadsto$ Plain $T$ ![](https://i.imgur.com/Dc9zk3N.png =320x100)
    * $\tau$ maps object $a$ to morphism $\tau_a$
    * $\tau$ maps morphism $f$ to commutative diagram: ![](https://i.imgur.com/WmiDL3l.png =200x100)

## 2.4 Constructing Datatypes

### Terminal Objects $1$

> A *terminal object* in a category $\mathcal{C}$ is an object $1$ such that for every object $A$ in $\mathcal{C}$ there is a unique morphism from $A$ to $1$, denoted by $!_A : 1 \leftarrow A$.
> 

> [Notation]
> $1$ will denote some fixed terminal object, and we will speak of **THE** terminal object.
> 

1. The *reflection* law: $!_1 = id_1$
2. The *fusion* law: $!_A \cdot f_{AB} = !_B$

The fusion law is equivalent to saying that the $!$ is a natural transformation $K_1 \leftarrow id$
![](https://i.imgur.com/TFi8xw8.png =300x200)

In **Fun**:
* The terminal object is a singleton set $\{p\}$.
* The morphism $!_A$ is the constant function maps every element of $A$ to $p$

In **JS**
* The terminal object can be identified with any JS value.
* The natural transformation $!$ is the combinator `S.K :: a -> b -> a`


### Initial Objects $0$

> A *initial object* in a category $\mathcal{C}$ is an object $I$ such that for every object $A$ in $\mathcal{C}$ there is a unique morphism from $I$ to $A$, denoted by $¡ : A \leftarrow I$.
> 

> [Notation]
> $0$ will denote some fixed initial object, and we will speak of **THE** initial object.
> 

1. The *reflection* law: $¡_0 = id_0$
2. The *fusion* law: $f_{AB} \cdot ¡_B = ¡_A$

The fusion law is equivalent to saying that the $¡$ is a natural transformation $id \leftarrow K_0$
![](https://i.imgur.com/R3A2300.png =300x180)


In **Fun**:
* The initial object is the empty set.
* The morphism $¡_A$ is the empty function.

In **Sanctuary.js**
* The initial object can be identified with values produced by infinite loop or throwing exceptions.
* The natural transformation $¡$ is a function than can never be called.

## 2.5 Products and Coproducts

### Spans, Projections and Products

Given objects $A, B$ in a category $\mathcal{C}$:

* The category $\text{Span}(A,B)$ of *spans* over $A$ and $B$ is a pair of morphisms $\left( f : A \leftarrow C, g : B \leftarrow C \right)$ with a common source.
* The objects are spans over $A$ and $B$.
* The morphisms $m : (f,g) \leftarrow (h,k)$ in $\text{Span}(A,B)$ are those of $\mathcal{C}$ such that the following diagram commutes.
* ![](https://i.imgur.com/TZsvNwL.png =250x150)
* The terminal object in $\text{Span}(A,B)$ is called the <span style="color:green">*projections*</span> of $A, B$.
* The common source of the projections is called the <span style="color:green">*product*</span> of $A, B$.


[Notation]

* The projections: $(outl:A \leftarrow A \times B, outr: \leftarrow A \times B)$
* The product: $A \times B$
* The unique morphism $\langle f,g \rangle = !_{(f,g)}$

![](https://i.imgur.com/ttHZEnd.png =250x150)


[Laws]
* The cancellation <span style="color:lightgray">(def of span)</span>:
    * $outl \cdot \langle f,g \rangle = f$
    * $outr \cdot \langle f,g \rangle = g$
* The reflection law <span style="color:lightgray">($!_1 = id_1$)</span>:
    * $\langle outl,outr \rangle = id_{A \times B}$
* The fusion law <span style="color:lightgray">($!_A\cdot f_{AB} = !_B$)</span>:
    * $\langle f,g \rangle \cdot m = \langle f\cdot m, g \cdot m \rangle$

**Fun**
* The product of two sets $A, B$ is the cartesion product of $A, B$.
* The unique morphism $\langle f,g \rangle$ is the functipn $pair (f,g)$ defined by $pair (f,g)\ c = (f\ c, g\ c)$

**Sanctuary.js**
* The product of two types `a`, `b` is `$.Pair (a) (b)`
* The constructor is `S.Pair :: a -> b -> Pair a b`
* The projections are `S.fst :: Pair a b -> a` and `S.snd :: Pair a b -> b`
* The unique morphism is `S.lift2 (S.Pair) :: (c -> a) -> (c -> b) -> c -> Pair a b` (also called the *factorizer*)


![](https://i.imgur.com/2o64jPj.png =300x300)

### Product as Functor

If each pair of objects in $\mathcal{C}$ has a product, then $\times$ can be made into a bifunctor $\mathcal{C} \leftarrow \mathcal{C} \times \mathcal{C}$ by defining:

> $f \times g = \langle f \cdot outl, g \cdot outr \rangle$

We have

* The absorption law: $(f \times g) \cdot \langle p,q \rangle = \langle f \cdot p, g \cdot q \rangle$
* The composition law: $(f \times g) \cdot (h \times k) = (f \cdot h) \times (g \cdot k)$


![](https://i.imgur.com/vxWzVb4.png =300x300)

* $outl, outr$ are natural transformations:
    * $outl : outl \leftarrow (\times)$
    * $outr : outr \leftarrow (\times)$

![](https://i.imgur.com/3whhwpR.png =300x180)

* `S.bimap` is the bifunctor $(\times)$ for morphisms.
* `S.bimap` for `S.Pair` can be defined as
    * `f => g => S.lift2 (S.Pair) (B(f)(S.fst)) (B(g)(S.snd))`

### Coproduct

> The product of $A, B$ in $\mathcal{C}^{op}$ is called the *coproduct* of $A, B$ in $\mathcal{C}$.
> 

[Notation]

* The object is denoted by $A + B$
* The morphisms are detnoed by $(inl:A+B \leftarrow A, inr:A+B \leftarrow B)$
* Given the common target $f,g$, the unique morphism $¡_{(f,g)}$ is denoted by $[f,g] : C \leftarrow A+B$, called *case f or g*.
* The bifunctor (if defined) $+$ is defined by $f+g = [inl \cdot f, inr \cdot g]$

[Laws]
* The cancellation <span style="color:lightgray">(def )</span>:
    * $[ f,g ] \cdot inl = f$
    * $[ f,g ] \cdot inr = g$
* The reflection law <span style="color:lightgray">($¡_1 = id_1$)</span>: $[ outl,outr ] = id_{A + B}$
* The fusion law <span style="color:lightgray">($f_{AB} \cdot ¡_B = ¡_A$)</span>: $m \cdot [ f,g ] = [ m\cdot f, m \cdot g ]$
* The absorption law: $[p,q] \cdot (f+g) = [p \cdot f, q \cdot g]$
* The composition law: $(f + g) \cdot (h + k) = (f \cdot h) + (g \cdot k)$

![](https://i.imgur.com/RY6IneI.png =300x180)

![](https://i.imgur.com/ooV07xl.png =300x300)

**Sanctuary.js**

![](https://i.imgur.com/JrriIeJ.png =300x180)

### Polynomial Functors

1. The *identity* functor $id : A ⟻ A,\ f ⟻ f$ is polynomial.
2. The *constant* functor $K_A : A ⟻ B,\ id_A ⟻ f$ is polynomial.
3. If $F,G$ are polynomial,
    1. their *composition* $FG : F(GA) ⟻ A,\ F(Gf) ⟻ f$ is polynomial.
    2. their *pointwise sum* $F+G : FA + GA ⟻ A,\ Ff + Gf ⟻ f$ is polynomial.
    3. their *pointwise product* $F \times G : FA \times GA ⟻ A,\ Ff \times Gf ⟻ f$ is polynomial.

## 2.6 Initial Algebras

Let $F : \mathcal{C} \leftarrow \mathcal{C}$ be a functor.

An ***$F$-algebra*** is an arrow of type $A \leftarrow FA$.

The object $A$ above is called the *carrier* of the algebra.

An *$F$-homomorphism*,
to <span style="color:lightgray">an algebra</span> $f : A \leftarrow FA$,
from <span style="color:lightgray">an algebra</span> $g : B \leftarrow FB$,
is an arrow $h : A \leftarrow B$ such that the following commutes:

![](https://i.imgur.com/KdjL2A1.png =150x150)

The ***$Alg(F)$*** is the category where objects are $F$-algebras, morphisms are $F$-homomorphisms.

An initial object of $Alg(F)$ (if exists) is called a ***initial algebra***.

> The polynomial functors of **Fun** always has a initial algebra!
> 

[Notation]

* An initial algebra of $F$ is denoted by $\alpha : T \leftarrow FT$
* The unique $F$-homomorphism to any other $F$-algebra $f : A \leftarrow FA$ is denoted by $¡_f = ⦇f⦈$, called a <span style="color:red">*catamorphism*</span>.
* 

![](https://i.imgur.com/2BhPyih.png =200x200)

[Laws]

* Reflection law: $¡_\alpha = ⦇\alpha⦈ = id_T$
* Fusion law: $h \cdot ⦇f⦈ = ⦇g \cdot f⦈$ <span style="color:lightgrey">for $h \cdot f = g \cdot Fh$</span>
* $\alpha$ is an isomorphism with inverse $⦇F\alpha⦈$

![](https://i.imgur.com/5zILIxu.png =330x400)![](https://i.imgur.com/G7ijyUl.png =300x400)

> Because $T \cong FT$ via $\alpha$, we called $(\alpha,T)$ a ***fixpoint*** of $F$.

In FP, we often use the notation:

```
          Fix/unFix
  Fix f <---------> f (Fix f)
      |              |
cata alg         fmap (cata alg)
      |              |
      v    alg       v
      a <---------- f a
```

### Natural Numbers

1. FP: `Nat := zero | succ Nat`
2. Type Functor:
    * $F = K_1 + id$
    * $FA = 1 + A$
    * $Fg = id_1 + g$
3. Algebra: $[c,f] : A \leftarrow 1 + A$
4. Diagram:![](https://i.imgur.com/G22fweP.png =240x200)
5. Catemorphism: $h = ⦇c,f⦈ = foldn(c,f)$
    * $h \cdot zero = c$
    * $h \cdot succ = f \cdot h$

### Strings: Lists of Characters

1. FP: `String := nil | cons (Char, String)`
2. Type Functor:
    * $F = K_1 + K_{Char} \times id$
    * $FA = 1 + Char \times A$
    * $Fg = id_1 + id_{Char} \times g$
3. Algebra: $[c,f] : A \leftarrow 1 + Char \times A$
4. Diagram: ![](https://i.imgur.com/Oi1t2Op.png =300x150)
5. Catamorphism: $h = ⦇c,f⦈ = foldr(c,f)$
    * $h \cdot nil = c$
    * $h \cdot (cons (x, xs)) = f (x, h\ xs)$

## 2.7 Type Functors

> $\alpha_A : TA \leftarrow F(A,TA)$
> 


| Structure                    | F                       | Initial Algebra |
| -------------------------    | ----------------------- | --------------- |
| $X \cong 1+X$                | $FX = 1+X$              | $Nat$           |
| $X \cong 1 + Char \times X$  | $FX = 1+Char \times X$  | $String$        |
| $X \cong 1 + A    \times X$  | $F_A X = 1+A \times X$  | $listr A$       |

The last one is parametrized by a type $A$!

### [Base Functor]

$F (A,X) = 1 + A \times X$

* as a functor:
    * $F_A (X) = 1 + A \times X$
    * $F_A (f) = id_1 + id_A \times f$
* as a **bifunctor**: ... called the *base functor*
    * $F (A,X) = 1 + A \times X$
    * $F (g,f) = 1 + g \times f$

### [Type Functor]

Consider the collection of $F (A,-)$-algebras with their initial algebras $\alpha_A$.

consider A morphism $f : B \leftarrow A$.

Via cata (fold), the *** type contstructor*** $T$ can be made into a functor (mappable) as:

$Tf = ⦇\alpha \cdot F(f,id)⦈$

![](https://i.imgur.com/2x2SDz7.png =300x300) ![](https://i.imgur.com/0QdBYqQ.png =280x280)

(identity?, composistion?)

From the same diagram above, we can see that the $\alpha : T \leftarrow G$, where $G(f) = F(f,Tf)$ is a **natural transformation**.


### [Type Fusion]

$⦇h⦈ \cdot Tg = ⦇h \cdot F(g,id)⦈$

> 其實相當直觀，見後範例的 3 顆樹 [圖](###trees)

![](https://i.imgur.com/mSRxSBU.png =400x400)


Proof:


1. 右下 diagram commutes because of the bifunctority of $F$.
2. 左下 diagram commutes by the definition of a cata for $h$.
3. 下半 diagram commutes because 右下 and 左下 does.
4. Therefore the whole diagarm commutes, or equivalently, $⦇h⦈ \cdot Tg = ⦇h \cdot F(g,id)⦈$ because of the cata's fusion law.

### Down to $listr A$:

1. FP: `listr A := nil | cons (A, listr A)`
2. Base Functor: $F\ X = 1 + A \times X$
3. Algebra: $[c, f]_A : T A \leftarrow 1 + A \times TA$
4. Initial: $[nil, cons]_A : listr A \leftarrow 1 + A \times (listr A)$
5. Diagram: ![](https://i.imgur.com/LPscb7u.png =200x100)
6. Catamorphism: ...
7. Type Functor: $listr f = ⦇\alpha \cdot F(f,id)⦈ = ⦇[nil,cons] \cdot (id_1+f \times id)⦈$
    * $listr\ f\ nil = nil$
    * $listr\ (cons (a,as)) = cons (f a, listr\ f\ as)$
8. Example of *type functor fusion*:
    * $sum = ⦇zero,plus⦈ : Nat \leftarrow listr Nat$
    * $sum \cdot listr f = ⦇zero,plus \cdot (f \times id)⦈$
    * ![](https://i.imgur.com/RywU48h.png =350x350)


> *A catamorphism (a fold) composed with its type functor (a map) can always be expressed as a single catamorphism*.
> 

#### trees

```mermaid
graph TD
    style m1 fill:#f9f,stroke:#333,stroke-width:4px
    style m2 fill:#f9f,stroke:#333,stroke-width:4px
    style m3 fill:#f9f,stroke:#333,stroke-width:4px
    
    style h1 fill:#f9f,stroke:#333,stroke-width:4px
    style h2 fill:#f9f,stroke:#333,stroke-width:4px
    style h3 fill:#f9f,stroke:#333,stroke-width:4px
    style nil3 fill:#f9f,stroke:#333,stroke-width:4px
    
    subgraph foldr_c_h_fmap_f_as
    h1[h] --> aa1[f n 1]
    h1[h] --> h2[h]
    h2[h] --> aa2[f n2]
    h2[h] --> h3[h]
    h3[h] --> aa3[f n3]
    h3[h] --> nil3[c]
    end
    
    subgraph fmap_f_as
    cons4[cons] --> m1[f n1]
    cons4[cons] --> cons5[cons]
    cons5[cons] --> m2[f n2]
    cons5[cons] --> cons6[cons]
    cons6[cons] --> m3[f n3]
    cons6[cons] --> nil2[nil]
    end
    
    subgraph as
    cons1[cons] --> n1
    cons1[cons] --> cons2[cons]
    cons2[cons] --> n2
    cons2[cons] --> cons3[cons]
    cons3[cons] --> n3
    cons3[cons] --> nil
    end
```

## Monad

A ***monad*** is ...
* an endofunctor $H : \mathcal{C} \leftarrow \mathcal{C}$ together with
* two natural transformations $\eta : H \leftarrow id$ and $\mu : H \leftarrow H^2$ such that the following diagrams commute.

![](https://i.imgur.com/c2ikZov.png =250x150) ![](https://i.imgur.com/aATstmp.png =150x150)

[NOTE]

The componets are given by

* $(H\mu)_x = H(\mu_x) : H^2x \leftarrow H^3x$
* $(\mu H)x = \mu_{Hx} : H^2x \leftarrow H^3x$

viz, the $H\mu$ and $\mu H$ are composed "horizentally".

---

Recall a ***monoid*** is ...
* a set $M$ together with
* two operators $\eta : M \leftarrow 1$ and $\mu : M \leftarrow M \times M$ such that the following diagrams commute.

![](https://i.imgur.com/npnxS7b.png =250x150) ![](https://i.imgur.com/0W6s6WT.png =150x150)

> We shall thus call $\eta$ the *unit* and $\mu$ the *multiplication* of the monad $H$; ...
> All told, a monad in $\mathcal{C}$ is just a monoid in the catogory of endofunctors of $\mathcal{C}$, with product $\times$ replaced by composition of endofunctors and unit set by the identity endofunctor.
> 

---

Pointwisely

Monad:
![](https://i.imgur.com/6nmgKCw.png =270x160) ![](https://i.imgur.com/qQDv35S.png =160x160)


Monoid:
![](https://i.imgur.com/bLfBk6T.png =250x150) ![](https://i.imgur.com/WFjklUp.png =150x150)


