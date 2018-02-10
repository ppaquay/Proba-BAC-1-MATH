---
title       : Distributions de probabilités discrètes
description : Nous allons dans ce chapitre explorer les concepts basiques du calcul des probabilités.


---
## Le lancer d'une pièce de monnaie (1)

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: c58587436b
```

Nous avons vu que si un évènement $E$ a une probabilité $p$ de se produire, il semble naturel lorsque l'expérience aléatoire est répétée un grand nombre de fois, que la fraction du temps où $E$ va se réaliser sera approximativement égale à $p$.

Par exemple, lors du lancer d'une pièce de monnaie bien équilibrée, nous nous attendons à ce que la probabilité d'obtenir pile soit de 1/2. D'après le raisonnement évoqué ci-dessus, si nous lancions une pièce de monnaie un grand nombre de fois, nous devrions voir que la proportion du nombre de lancers où pile apparaît est égale à 1/2.

Nous allons simuler ce phénomène aléatoire et examiner les résultats obtenus.


`@instructions`
- Initialisez le générateur de nombres pseudo-aléatoires à l'aide de la fonction `set.seed()` avec la valeur 1.
- Définissez un vecteur `piece` qui compte deux éléments `"Pile"` et `"Face"`.
- Utilisez la fonction `sample()` avec l'option `replace = TRUE` pour simuler le lancer de la pièce de monnaie 10 fois d'affilée. Nommez votre résultat `lancers_10`.
- Affichez les 5 premiers éléments du vecteur `lancers_10` à l'aide de la fonction `head()`.
- Calculez la proportion du nombre de lancers où on a obtenu pile à l'aide de la fonction `mean()` qui calcule la moyenne. Nommez votre résultat `prop_10`.

`@hint`
- Pour définir le vecteur `piece`, utilisez la fonction `c()`.
- La fonction `sample()` prend deux paramètres : le vecteur `piece`, le nombre de lancers `10` et l'option `replace = TRUE`.
- N'oubliez pas de calculer la moyenne uniquement pour les valeurs pile, c'est-à-dire `lancers10 == "Pile"`.

`@sample_code`
```{r}
# Initialisation du générateur aléatoire


# Définition du vecteur 'piece'


# Simulation de 10 lancers de la pièce de monnaie
lancers_10 <- sample(___, ___, replace = TRUE)

# Premiers éléments de 'lancers_10'


# Proportion de piles obtenus
prop_10 <- mean(___)

```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition du vecteur 'piece'
piece <- c("Pile", "Face")

# Simulation de 10 lancers de la pièce de monnaie
lancers_10 <- sample(piece, 10, replace = TRUE)

# Premiers éléments de 'lancers_10'
head(lancers_10)

# Proportion de piles obtenus
prop_10 <- mean(lancers_10 == "Pile")

```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
test_function("set.seed", args = "seed",
              not_called_msg = "Vous n'avez pas utilisé la fonction `set.seed()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `set.seed(seed = ...)` avec l'argument 1.")
              
test_object("piece",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `piece`.")

test_object("lancers_10",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `lancers_10`. Avez-vous bien précisé tous les paramètres ?")

test_function("head", args = "x",
              not_called_msg = "Vous n'avez pas utilisé la fonction `head()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `head(x = ...)` avec les arguments corrects.")

test_function("sample", args = c("x", "size", "replace"),
              not_called_msg = "Vous n'avez pas utilisé la fonction `sample()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `sample(x = ..., taille = ..., replace = TRUE)` avec les arguments corrects.")
              
test_function("mean", args = "x",
              not_called_msg = "Vous n'avez pas utilisé la fonction `mean()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `mean(x = ...)` avec les arguments corrects.")

test_object("prop_10",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `prop_10`. Avez-vous bien précisé tous les paramètres ?")

test_error(incorrect_msg = "Une erreur est présente dans votre code source.")

success_msg("Bravo ! Il nous reste maintenant à calculer la proportion de piles obtenue pour un nombre variable de lancers.")
```

---
## Le lancer d'une pièce de monnaie (2)

```yaml
type: NormalExercise
key: eeafc22f7b
lang: r
xp: 100
skills: 1
```
Nous allons maintenant écrire une fonction qui prend comme arguments notre vecteur `piece`, le nombre de lancers et qui donne comme résultat la proportion de piles obtenus. Cette manière de procéder a l'avantage de produire du code que nous pourrons réutiliser directement.

Le vecteur `piece` est déjà défini dans votre espace de travail.

`@instructions`
- Initialisez ici encore le générateur de nombres pseudo-aléatoires à l'aide de la fonction `set.seed()` avec la valeur 1.
- Complétez le corps de la fonction `prop_n()` qui prend comme arguments un vecteur `vec` et un nombre `n` de lancers.
- Testez votre fonction avec le vecteur `piece` et un nombre de lancers égal à 100, 1000 et 10000 successivement. Nommez ces résultats par `prop_100`, `prop_1000` et `prop_10000` respectivement. N'oubliez pas d'afficher vos résultats.

`@hint`
- Pour compléter le corps de la fonction `prop_n()`, inspirez-vous de l'exercice précédent.

`@pre_exercise_code`
```{r}
piece <- c("Pile", "Face")
```

`@sample_code`
```{r}
# Initialisation du générateur aléatoire


# Définition de la fonction 'prop_n()'
prop_n <- function(vec, n) {
  lancers_n <- sample(___, ___, replace = TRUE)
  prop_n <- mean(___)
  
  return(prop_n)
}

# Proportion de piles pour 100 lancers
prop_100 <- prop_n(___, ___)
prop_100

# Proportion de piles pour 1000 lancers


# Proportion de piles pour 10000 lancers


```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition de la fonction 'prop_n()'
prop_n <- function(vec, n) {
  lancers_n <- sample(vec, n, replace = TRUE)
  prop_n <- mean(lancers_n == "Pile")
  
  return(prop_n)
}

# Proportion de piles pour 100 lancers
prop_100 <- prop_n(piece, 100)
prop_100

# Proportion de piles pour 1000 lancers
prop_1000 <- prop_n(piece, 1000)
prop_1000

# Proportion de piles pour 10000 lancers
prop_10000 <- prop_n(piece, 10000)
prop_10000

```

`@sct`
```{r}
test_function("set.seed", args = "seed",
              not_called_msg = "Vous n'avez pas utilisé la fonction `set.seed()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `set.seed(seed = ...)` avec l'argument 1.")
              
test_object("prop_100",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `prop_100`. Avez-vous bien précisé tous les paramètres ?")
            
test_object("prop_1000",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `prop_1000`. Avez-vous bien précisé tous les paramètres ?")
            
test_object("prop_10000",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `prop_10000`. Avez-vous bien précisé tous les paramètres ?")

test_error(incorrect_msg = "Une erreur est présente dans votre code source.")

success_msg("Très bien ! Nous constatons que les proportions obtenues sont de plus en plus proche de 0.5. Nous allons maintenant représenter le graphique de la fonction qui donne la proportion de piles obtenue en fonction du nombre de lancers.")
```

---
## Le lancer d'une pièce de monnaie (3)

```yaml
type: NormalExercise
key: 83e9502afb
lang: r
xp: 100
skills: 1
```
Il est maintenant temps de tracer le graphe de la fonction qui donne la proportion de piles obtenue en fonction du nombre de lancers.

Le vecteur `piece` et la fonction `prop_n()` sont déjà définis dans votre espace de travail.

*N.B.* La fonction `prop_n()` définie dans l'exercice précédent a ici été modifiée pour accepter des arguments vectoriels.

`@instructions`
- Initialisez ici encore le générateur de nombres pseudo-aléatoires à l'aide de la fonction `set.seed()` avec la valeur 1.
- Définissez un vecteur `lancers` qui contient le nombre de lancers différents à l'aide de la fonction `seq()` qui débute à 1 jusque 10000 par bonds de 10.
- Définissez un vecteur `prop_piles` qui contient la proportion de piles obtenues en fonction du nombre de lancers à l'aide de votre fonction `prop_n()` et les arguments `piece` et `lancers`.
- Représentez le graphe de la fonction `prop_n()` à l'aide de la fonction `plot()` avec les arguments suivants : `lancers` pour les abscisses, `prop_pile` pour les ordonnées, `"Nbre de lancers"` pour le nom de l'axe des abscisses et `"Proportion de piles"` pour le nom de l'axe des ordonnées.
- Tracez la droite d'équation $y = 0.5$ à l'aide de la fonction `abline()` et les arguments suivants : `0.5` pour l'ordonnée à l'origine et `0` pour la pente.


`@hint`
- La fonction `seq()` prend comme arguments le premier et le dernier éléments de la séquence, et le troisième argument correspond aux bonds entre chaque élément de la séquence.

`@pre_exercise_code`
```{r}
piece <- c("Pile", "Face")
prop_n <- function(vec, n) {
  lancers_n <- sample(vec, n, replace = TRUE)
  prop_n <- mean(lancers_n == "Pile")
  
  return(prop_n)
}
prop_n <- Vectorize(prop_n, vectorize.args = "n")
```

`@sample_code`
```{r}
# Initialisation du générateur aléatoire


# Définition des vecteurs 'lancers' et 'prop_piles'
lancers <- seq(___, ___, by = ___)
prop_piles <- prop_n(___, ___)

# Tracé du graphique de la fonction 'prop_n()'
plot(___, ___, xlab = ___, ylab = ___, type = "l", col = "blue")
abline(___, ___, col = "red", lty = 2)
```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition des vecteurs 'lancers' et 'prop_piles'
lancers <- seq(1, 10000, by = 10)
prop_piles <- prop_n(piece, lancers)

# Tracé du graphique de la fonction 'prop_n()'
plot(lancers, prop_piles, xlab = "Nbre de lancers", ylab = "Proportion de piles", type = "l", col = "blue")
abline(0.5, 0, col = "red", lty = 2)
```

`@sct`
```{r}
test_function("set.seed", args = "seed",
              not_called_msg = "Vous n'avez pas utilisé la fonction `set.seed()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `set.seed(seed = ...)` avec l'argument 1.")
              
test_object("lancers",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `lancers`. Avez-vous bien précisé tous les paramètres ?")
            
test_object("prop_piles",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `prop_piles`. Avez-vous bien précisé tous les paramètres ?")
            
test_function("plot", args = c("x", "y", "xlab", "ylab"),
              not_called_msg = "Vous n'avez pas utilisé la fonction `plot()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `plot(x = ..., y = ...)` avec les arguments demandés.")
              
test_function("abline", args = c("a", "b"),
              not_called_msg = "Vous n'avez pas utilisé la fonction `abline()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `abline(a = ..., b = ...)` avec les arguments demandés.")
            
test_error(incorrect_msg = "Une erreur est présente dans votre code source.")

success_msg("Bravo ! Comme prévu, nous constatons clairement que plus le nombre de lancers augmente plus nous nous rapprochons de la proportion 1/2 attendue.")
```

---
## Lancer de deux dés à quatre faces (1)

```yaml
type: NormalExercise
key: dcec008e23
lang: r
xp: 100
skills: 1
```
Nous allons maintenant nous intéresser au phénomène aléatoire qui consiste à lancer deux dés à quatre faces bien équilibrés.

Pour ce faire, nous allons construire une fonction `lancers_2des` qui prend comme argument un nombre de lancers et qui donne le résultat de ces lancers.

`@instructions`
- Initialisez le générateur de nombres pseudo-aléatoires à l'aide de la fonction `set.seed()` avec la valeur 1.
- Définissez un vecteur `de` qui contient les nombres de 1 à 4.
- Complétez le corps de la fonction `lancers_2des()` qui prend comme arguments un nombre `n` de lancers. N'oubliez pas d'utiliser la fonction `sample()` avec l'option `replace = TRUE` pour simuler le lancer du dé n fois d'affilée.
- Affichez le résultat du lancer des deux dés 10 fois de suite. Vous devez d'abord définir un vecteur `lancers10` qui contient le résultat des 10 lancers des deux dés, et ensuite vous affichez son contenu.

`@hint`
- Pour définir le vecteur `de`, vous pouvez utiliser la fonction `c()`.
- Les arguments de la fonction `sample()` sont d'abord le vecteur `de` et ensuite le nombre `n` de répétitions.
- Pour afficher le résultat des 10 lancers, il suffit d'utiliser la fonction `lancers_2des()` avec l'argument 10 pour créer le vecteur `lancers10` et ensuite de l'afficher.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Initialisation du générateur aléatoire


# Définition du vecteur 'de'


# Définition de la fonction 'lancers_des()'
lancers_2des <- function(n) {
  df <- data.frame(de1 = ___(___, ___, replace = TRUE), de2 = ___(___, ___, replace = TRUE))
  
  return(df)
}

# Résultat de 10 lancers des deux dés


```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition du vecteur 'de'
de <- 1:4

# Définition de la fonction 'lancers_2des()'
lancers_2des <- function(n) {
  df <- data.frame(de1 = sample(de, n, replace = TRUE), de2 = sample(de, n, replace = TRUE))
  
  return(df)
}

# Résultat de 10 lancers des deux dés
lancers10 <- lancers_2des(10)
lancers10
```

`@sct`
```{r}
test_function("set.seed", args = "seed",
              not_called_msg = "Vous n'avez pas utilisé la fonction `set.seed()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `set.seed(seed = ...)` avec l'argument 1.")
              
test_object("de",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `de`. Avez-vous bien précisé tous les paramètres ?")
            
test_object("lancers10",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `lancers10`. Avez-vous bien précisé tous les paramètres ?")
            
test_error(incorrect_msg = "Une erreur est présente dans votre code source.")

success_msg("Très bien ! Nous avons maintenant à notre disposition une fonction qui va nous permettre de calculer diverses probabilités concernant ces deux dés.")
```

---
## Lancer de deux dés à quatre faces (2)

```yaml
type: NormalExercise
key: 04f5786102
lang: r
xp: 100
skills: 1
```
Nous sommes maintenant prêts à calculer les probabilités de divers évènements en lien avec le lancer des deux dés à quatre faces.

Le vecteur `de` et la fonction `lancers_2des()` sont déjà définis dans votre espace de travail.

`@instructions`
- Initialisez le générateur de nombres pseudo-aléatoires à l'aide de la fonction `set.seed()` avec la valeur 1.
- Utilisez la fonction `lancers_2des()` pour définir un tableau `lancers_10000` qui contient les résultats de 10000 lancers des deux dés.
- Avec ce tableau et la fonction `mean()`, calculez la probabilité (ou proportion dans notre cas) que le résultat du premier dé soit égal au second.
- De même, calculez la probabilité que le résultat du premier dé soit supérieur au second.
- De même, calculez la probabilité que la somme des résultas des deux dés soit paire.

`@hint`
- La fonction `mean()` calcule la proportion des résultats vérifiant la caractéristique précisée.
- L'opérateur `$` permet de sélectionner une colonne d'un tableau (ici le premier ou le second dé).
- Un nombre est pair si le reste de sa division par 2 est 0. L'opérateur `%%` permet de calculer le reste de la division de deux nombres.

`@pre_exercise_code`
```{r}
de <- 1:4

lancers_2des <- function(n) {
  df <- data.frame(de1 = sample(de, n, replace = TRUE), de2 = sample(de, n, replace = TRUE))
  
  return(df)
}
```

`@sample_code`
```{r}
# Initialisation du générateur aléatoire


# Définition du tableau 'lancers_10000'


# Probabilité que dé1 = dé2
mean(___$de1 == ___$de2)

# Probabilité que dé1 > dé2
mean(___ > ___)

# Probabilité que dé1 + dé2 soit paire
mean((___ + ___) %% 2 == ___)
```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition du tableau 'lancers_10000'
lancers_10000 <- lancers_2des(10000)

# Probabilité que dé1 = dé2
mean(lancers_10000$de1 == lancers_10000$de2)

# Probabilité que dé1 > dé2
mean(lancers_10000$de1 > lancers_10000$de2)

# Probabilité que dé1 + dé2 soit paire
mean((lancers_10000$de1 + lancers_10000$de2) %% 2 == 0)
```

`@sct`
```{r}
test_function("set.seed", args = "seed",
              not_called_msg = "Vous n'avez pas utilisé la fonction `set.seed()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `set.seed(seed = ...)` avec l'argument 1.")
              
test_object("lancers_10000",
            incorrect_msg = "Vous n'avez pas défini correctement l'objet `lancers_10000`. Avez-vous bien précisé tous les paramètres ?")
            
test_function_result("mean",
                     index = 1,
                     not_called_msg = "Vous n'avez pas utilisé la fonction `mean()` !",
                     incorrect_msg = "Votre première fonction `mean()` ne donne pas le résultat correct, vérifiez votre argument !")
                     
test_function_result("mean",
                     index = 2,
                     not_called_msg = "Vous n'avez pas utilisé la fonction `mean()` !",
                     incorrect_msg = "Votre deuxième fonction `mean()` ne donne pas le résultat correct, vérifiez votre argument !")
                     
test_function_result("mean",
                     index = 3,
                     not_called_msg = "Vous n'avez pas utilisé la fonction `mean()` !",
                     incorrect_msg = "Votre troisième fonction `mean()` ne donne pas le résultat correct, vérifiez votre argument !")
              
test_error(incorrect_msg = "Une erreur est présente dans votre code source.")

success_msg("Bon travail !")
```

---
## Le pari du chevalier De Méré (1)

```yaml
type: NormalExercise
key: d68768086e
lang: r
xp: 100
skills: 1
```
Le chevalier De Méré (1607-1684), qui était un joueur invétéré, avait l'habitude de parier que, sur quatre lancers d'un dé, la valeur six allait apparaître au moins une fois.

Nous allons donc vérifier cette affirmation en calculant la probabilité de cet évènement.

`@instructions`

`@hint`

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition du vecteur 'de'
de <- 1:6

# Définition de la fonction 'lancers_4des()'
lancers_4des <- function(n) {
  df <- data.frame(lancer1 = sample(de, n, replace = TRUE),
                   lancer2 = sample(de, n, replace = TRUE),
                   lancer3 = sample(de, n, replace = TRUE),
                   lancer4 = sample(de, n, replace = TRUE))
                   
  return(df)
}

# Définition du vecteur 'lancers_10000'
lancers_10000 <- lancers_4des(10000)

# Premiers éléments de 'lancers_10000'
head(lancers_10000)

```

`@sct`
```{r}

```
