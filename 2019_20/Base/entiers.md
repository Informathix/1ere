# Rerésentations des entiers naturels en bases 2 et 16

## Écriture d'un entier en base b

>#### Definition
>Une base est un entier naturel $\beta$ supérieur ou égal à deux.  

>Dire qu'un
>nombre s'ecrit $a_na_{n-1}a_{n-2}...a_1a_{0_\beta}$ en base $\beta$ signifie qu'il
>est égal à 
>$$a_n\times\beta^n      +      a_{n-1}\times\beta^{n-1}+
>a_{n-2}\times\beta^{n-2}+\cdots+a_1\times\beta+a_0
>$$
>avec les $a_i$ des entiers naturels strictement inférieurs à $\beta$.


Par  exemple,  $237_{10}$  est égal  à  $2\times10^2  +  3\times  10 +  7$  mais
$237_8=2\times8^2 + 3\times 8 + 7=159_{10}$.


## Les bases privilégiées en informatique

En  informatique, on  travaille  en base  2  (les bits),  en  base 16  (adresses
mémoire, couleurs HTML) et parfois en base 8 (droits des fichiers UNIX).

### Écriture en base 16

On ne dispose pas d'assez de chiffres pour écrire les 16 chiffres de la base 16.

Les  10 premiers  sont les  mêmes qu'en  base 10.  Ensuite on  utilise les  cinq
premières lettres de l'alphabet:


~~~
base 10 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 
base 16 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

base 10 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 |
base 16 | A  | B  | C  | D  | E  | F  | 10 | 11 |
~~~

### Conversion de la base 10 vers la base 2

#### algorithme de soustraction

On retranche du nombre la plus grande puissance de 2 possible :


<!--
- $1347_{10} -$ **1** $\times 2^{10} = 1347_{10} - 1024_{10} = 323_{10}$ : **1**
- $323_{10} -$ **0** $\times 2^{9} = 323_{10}$ : **0**
- $323_{10} -$ **1** $\times 2^{8} = 323_{10}-256_{10} = 67_{10}$: **1**
- $67_{10} -$ **0** $\times 2^{7} = 67_{10}$ : **0**
- $67_{10} -$ **1** $\times 2^{6} = 67_{10}-64_{10} = 3_{10}$: **1**
- $3_{10} -$  **0** $\times 2^{5} = 3_{10}$ : **0**
- $3_{10} -$ **0** $\times 2^{4} = 3_{10}$ : **0**
- $3_{10} -$ **0** $\times 2^{3} = 3_{10}$ : **0**
- $3_{10} -$ **0** $\times 2^{2} = 3_{10}$ : **0**
- $3_{10} -$ **1** $\times 2^{1} = 3_{10}-2_{10} = 1_{10}$: **1**
- $1_{10} -$ **1** $\times 2^{0} = 1_{10}-1_{10} = 0_{10}$: **1**
- donc $1347_{10} = \mathbf{10101000011}_2$

-->

- 58~10~ - **1** x 2^5^ = 58~10~ - 32~10~ = 26~10~   => **1**
- 26~10~ - **1** x 2^4^ = 10~10~   => **1**
- 10~10~ - **1** x 2^3^ = 2~10~  => **1**
- 2~10~ - **0** x 2^2^ = 2~10~  => **0**
- 2~10~ - **1** x 2^1^ = 0  => **1**
- 0~10~ - **0** x 2^0^ = 0  => **0**
- 
donc 58~10~ = 111010~2~

#### Algorithme de division


On écrit les divisions successives du nombre par 2 puis des quotients successifs
obtenus par 2 également.

En lisant les restes de bas en haut on obtient le même résultat.

*On obtient  par ce  même algorithme de la division  la conversion  de la  base 10  en n'importe
quelle autre base.*

### Conversion de la base 2 vers la base 16

On groupe les bits par paquets de 4, quitte à rajouter des 0 à gauche:

${10101000011}_2={\underbrace{0101}_5/\underbrace{0100}_4/\underbrace{0011}_3}={543}_{16}$

## Conversion de la base 16 vers la base 2

On transforme chaque caractère par un groupe de 4 bits:

$A3C_{16}=1010/0011/1100={101000111100}_2$


### Conversion de la base 16 à la base 10

On  écrit les  caractères  en base  10  et  on utilise  la  définition avec  les
puissances de la base de départ, ici 16 :

$A3C_{16}=10_{10}\times    16^2     +    3_{10}\times     16^1+    12_{10}\times
16^0=10_{10}\times 256_{10}+3_{10}\times 16_{10}+12_{10}=2620_{10}$

*On obtient par  le même algorithme la conversion de  n'importe quelle base vers
la base 10*

## Avec Python

```Python
>>> 0xa3c # préfixe 0x pour la base 16
2620

>>> 0b10101000011 # préfixe 0b pour la base 2
1347

>>> 0o775 #préfixe 0o pour la base 8
509
```

et inversement:

```Python

>>> bin(1347)
'0b10101000011'

>>> hex(2620)
'0xa3c'

>>> oct(509)
'0o775'
```

On peut également  demander la conversion en  base 10 de tout  nombre écrit dans
une base comprise entre 2 et 36 avec la syntaxe `int('nombre en base b', b)`


```Python
>>> int('a3c',16)
2620

>>> int('123',4)
27

>>> int('zzz',36)
46655
```



## Exercices

### Exercice 1 : Conversion entre plusieurs bases

Complétez le tableau suivant :

| base 2 | base 10 | base 16 |
| ------ | ------- | ------- |
| 100010 |         |         |
| 110010 |         |         |
|        | 37      |         |
|        | 1023    |         |
|        |         | 1E      |
|        |         | FF0     |

## Exercice 2 : Taille des nombres entiers positifs en bases 2 et 16

Si on utilise $n$ chiffres binaires, on peut représenter tous les nombres de 0 à $2^n-1$.
Vérifiez cette affirmation pour quelques valeurs de $n$ : 2, 3 et 8.

Inversement, combien faut-il de chiffres binaires pour pouvoir représenter tous les nombres entiers de 0 à 19999 ?
Combien faut-il de chiffres hexadécimaux pour représenter les mêmes nombres ?

## Exercice 3 : Additions binaires

Effectuez en binaire les additions des nombres entiers positifs suivants :

* 11010 + 100001
* 11100010 + 10011
* 10100011 + 11100111
* 11111 + 11111


## Exercice 4 : 8 bits sur Python

Un entier  en base 16 peut  être introduit en  Python en le faisant  précéder de
`0x` :

```python
In [25]: 0xa1
Out[25]: 161  
```

Un entier  en base 2 peut  être introduit en  Python en le faisant  précéder de
`0b`:

```python
In [26]: 0b1101
Out[26]: 13  
```


L'opérateur `&` entre deux entiers  $a$ et $b$ crée un entier
dont les bits sont positionnées à 1 si, et seulement si, ils sont positionnées à
1 dans $a$ et $b$.


```python
In [31]: 0b11 & 0b111000110101
Out[31]: 1

In [32]: 0b11 & 0b111000110111
Out[32]: 3

In [33]: 0b11 & 0b11100011011111011
Out[33]: 3

In [34]: 0b11 & 0b1110001101111101100
Out[34]: 0  
```


Imaginez alors un moyen de calculer sur des entiers 8 bits non signés en Python.




## Exercice 5 : décomposition en base quelconque

Trouvez une fonction `base(b,n)` qui renvoie la liste des
chiffres de l'écriture normalisée de $n$ en base $b$ avec $1<b<10$.

```python
In [1]: base(2,97) 
[1, 1, 0, 0, 0, 0, 1]
```

## Exercice 6 : écriture littérale

 Déterminez une  fonction qui renvoie l'écriture  littérale d'un nombre
 dont l'écriture décimale est comprise entre 1 et 999.
 
 
## Exercice 7 : Bibinaire

Boby   Lapointe,  célèbre   chanteur   français,  était   aussi
mathématicien à ses heures. Ayant  trouvé le code binaire trop compliqué
à utiliser, il inventa le  code... bibinaire. Il suffit de remplacer les
chiffres  par des lettres.  On commence  par couper  le nombre  écrit en
binaire en  paquets de  2.  S'il y  a un  nombre impair de  chiffres, on
rajoute un zéro à gauche, ce qui ne modifie pas la valeur de nombre.  On
commence par le premier
groupe de deux chiffres  le plus à droite. On remplace 00  par O, 01 par
A, 10 par E, 11 par I.

Puis on  prend le paquet  de deux chiffres  suivants en se  déplaçant de
droite à gauche. On remplace 00
par H, 01 par B, 10 par K, 11 par D.

Pour le paquet suivant, on recommence avec les voyelles. S'il y a encore
un groupe, on remplace par une consonne, etc.




Écrivez  les nombres  de  0 à  25  en bibinaire.   Pourquoi Boby  a-t-il
finement choisi le H?

Écrivez la table de 3 en bibinaire.


Écrivez les  nombres de  255 à 257  en bibinaire.   Quel est la  base du
bibinaire? Écrivez 355 en bibinaire.

Écrivez KEKIDI et HEHOBOBI en base 10.

Pourquoi est-il pratique  d'écrire les nombres en base  2 avec un nombre
de chiffres multiple de 4 avant de les traduire en bibinaire?


Il ne vous reste plus qu'à écrire un traducteur bibinaire en Python...
