# tipe_marches_aleatoires
# Retours à l'origine d'une marche aléatoire sur $\mathbb{Z}^d$

TIPE réalisé durant mon année de 5/2. 
[Présentation du TIPE (PDF)](presentation-tipe.pdf)

## Problématique

Quelle est la probabilité qu'une marche aléatoire revienne à l'origine sur $\mathbb{Z}^d$ ?

## Contenu

### 1. Dimension 1
- Modélisation de la marche symétrique $S_n = \sum_{k=1}^{n} X_k$, avec $X_k \in \{-1, 1\}$ équiprobables.
- Loi de la position :

$$P(S_{2n} = 0) = \frac{1}{2^{2n}} \binom{2n}{n} \underset{n \to +\infty}{\sim} \frac{1}{\sqrt{\pi n}}$$

- Nombre de retours à l'origine $R_n$ après $2n$ pas :

$$\mathbb{E}(R_n) = \sum_{k=0}^{n} \frac{1}{4^k} \binom{2k}{k} = \frac{2n+1}{4^n} \binom{2n}{n} \underset{n \to +\infty}{\sim} 2\sqrt{\frac{n}{\pi}}$$

- Calcul de la variance de $R_n$, puis comparaison avec une simulation Python (moyenne empirique de $R_n$ encadrée par $\mathbb{E}(R_n) \pm \sigma(R_n)$).

### 2. Dimension $d \geqslant 2$
- Critère de récurrence : la marche est récurrente si et seulement si $\sum_n P(S_{2n} = 0)$ diverge.
- Théorème de Pólya (1921) : la marche est récurrente si et seulement si $d = 1$ ou $d = 2$.
- En dimension 2, $P(S_{2n} = 0) \sim \dfrac{1}{\pi n}$ : la série harmonique diverge, donc la marche est récurrente.
- Pour $d \geqslant 3$, $P(S_{2n} = 0) = O\left(n^{-d/2}\right)$ : la marche est transiente.

### 3. Marche piégée sur $\mathbb{Z}$
- Modélisation d'un piège sur le site $s$, de biais $p \in \,]0, 1[$ : en $s$, la marche va à gauche avec probabilité $p$ et à droite avec probabilité $1 - p$ ; ailleurs, elle est symétrique.
- Obtention de la loi de $X_n$ de proche en proche, grâce à la formule des probabilités totales.
- Comparaison entre marche symétrique et marche piégée : le piège augmente le nombre moyen de retours à l'origine.
- Comparaison théorie / simulation sur 2000 marches (piège en $s = 2$, $p = 0{,}9$).

## Code

Le code Python (annexe de la présentation) contient notamment :

| Fonction | Rôle |
|---|---|
| `RetourOrigine(n)` | Compte les retours à l'origine d'une marche sur $\mathbb{Z}$ après $2n$ pas |
| `Moyenne(n)`, `Esperance(n)`, `Variance(n)` | Moyenne empirique, espérance et variance de $R_n$ |
| `loi_Xn(n, s, p)` | Loi de $X_n$ pour la marche piégée, construite de proche en proche |
| `esperance_Xn(n, s, p)` | Position moyenne de la marche piégée |
| `simulation_marche(n, s, p)` | Simule une marche piégée |
| `esperance_nb_retours(n, s, p)` | Espérance théorique du nombre de retours à l'origine (marche piégée) |

Exemple :

```python
>>> loi_Xn(5, 2, 9/10)   # n pas, site du piège, biais
{-5: 0.03125, -3: 0.15625, -1: 0.3375, 1: 0.4375, 3: 0.03125, 5: 0.00625}
```

## Utilisation

```bash
pip install numpy scipy matplotlib
python tipe_marche_aleatoire.py
```

## Contenu du dépôt

```
├── README.md
├── presentation-tipe.pdf
└── tipe_marche_aleatoire.py
```



