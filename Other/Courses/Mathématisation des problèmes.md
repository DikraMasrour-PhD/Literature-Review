---
Professor: Prof. Ammar Oulamara
tags:
  - Course
  - Research
---
### Algorithmes & complexité
#### Paradigme: Divide & Conquer
**Temps d'exécution** d'un algorithme; règles générales:
- t.e d'une affectation ou d'un test est considéré constant C
- t.e d'une séquences d'instructions est la somme des t.e des instructions qui la composent
- t.e d'un branchement conditionel est le t.e du test + le max t.e des alternatives
**Divide & Conquer** étapes
- décomposition
- résolution
- recombinaison
	Complexité d'un algo divide & conquer: $T(n) = a.T(\frac{n}{b}) + D(n) + C(n)$ ; le problème est décomposé en $a$ sous-prob chacun de taille $\frac{n}{b}$ et $D(n)$ le temps nécessaire à la décomposition et $C(n)$ le temps nécessaire à la recomposition 
#### Dynamic Programming
**Bellman principle** Toutes sous-solution de la solution optimale est optimale. Composer une solution optimale du probleme en combinant les solutions (optimales) des ses sous-problemes.
- La prog dynamique n'est pas applicable a tout probleme. Seul un probleme dont les sous-problemes adoptent la meme structure en engendrant de la redondance de calcul. (e.g. Cacul de $C_{n}^k$)
> [!example] 
> Problème du sac à dos avec programmation dynamique
#### Greedy Algorithms / Algorithmes gloutons
- **Matroids** type of problems that accept a greedy algorithm for an optimal solution (see mathematical definition in slides)


> [!tip] Problem & Algorithm complexity
> Problem complexity(computational compexity) != Algorithm complexity
#### Problem complexity (computational compexity): P & NP problems
##### Problem
**Definition** A problem is composed of 
- un ensemble d'objets mathematiques: "instances"
	- e.g. probleme du voyageur de commerce etant donne ces villes et les distances entre elles
- une question liée a l'ensemble d'instances
- une (un ensemble de) solutions(s) pour chaque instance
**Types of problems**
- Probleme d'optimisation (also called property): e.g. le chemin qui minimise la distance parcourue >> solution x qui optimise (max / min) f(x)
- Probleme de decision: e.g. existe-t-il un chemin qui constitue un cycle hamiltonien de moins de 200 de distance>> OUI ou NON
**How do they relate?**
- Finding a solution for a optimisation problems tells us whether the decision problem has a solution or not and vice versa
- The two types of problems are equivalent in terms of complexity
##### Computational complexity of a problem
Computational complexity of a problem is the complexity in the worst case of best (least costly) algorithm that solves it
**Classes of problems**
- A problem is of **Class P** 'Practicable' , there exists an algorithm that resolves it in polynomial time. 
- **Class NP** 'Non Practicable' contains **Class P** 'Practicable' (e.g. )
	- HOW?
		- For P problems, we know an algorithm that *solves* the problem in polynomial time
		- For NP problems, we do not have an algorithm that solves the problem in polynomial time, but are able to *verify* a given solution in polynomial time
	- Definition of NP problems with certificate