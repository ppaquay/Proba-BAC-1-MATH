---
title       : Distributions de probabilités discrètes
description : Nous allons dans ce chapitre explorer les concepts basiques du calcul des probabilités.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


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


# Définition du vecteur piece


# Simulation de 10 lancers de la pièce de monnaie
lancers_10 <- sample(___, ___, replace = TRUE)

# Premiers éléments de lancers_10


# Proportion de piles obtenus
prop_10 <- mean(___)

```

`@solution`
```{r}
# Initialisation du générateur aléatoire
set.seed(1)

# Définition du vecteur piece
piece <- c("Pile", "Face")

# Simulation de 10 lancers de la pièce de monnaie
lancers_10 <- sample(piece, 10, replace = TRUE)

# Premiers éléments de lancers_10
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


# Définition de la fonction prop_n()
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

# Définition de la fonction prop_n()
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

success_msg("Très bien ! Nous constatons que les proportions obtenues sont de plus en plus proche de 0.5. Nous allons maintenant représenter le graphique qui donne la proportion de piles obtenue en fonction du nombre de lancers.")
```
