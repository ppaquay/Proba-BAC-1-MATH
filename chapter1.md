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
- Initialisez le générateur de nombres pseudo-aléatoires avec la fonction `set.seed()` avec la veleur 1.
- Définissez un vecteur `piece` qui compte deux éléments `"Pile"` et `"Face"`.
- Utilisez la fonction `sample()` avec l'option `replace = TRUE` pour simuler le lancer de la pièce de monnaie 10 fois d'affilée. Nommez votre résultat `lancers_10`.
- Affichez les 5 premiers éléments du vecteur `piece` à l'aide de la fonction `head()`.
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


# Premiers éléments de lancers_10


# Proportion de piles obtenus

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
test_function("set.seed", args = 1,
              not_called_msg = "Vous n'avez pas utilisé la fonction `set.seed()` !"
              incorrect_msg = "Vous n'avez pas utilisé la fonction `set.seed(seed = ...)` avec l'argument 1.")
              
test_object("piece")

test_object("lancers_10")

test_function("head", args = "lancers_10",
              not_called_msg = "Vous n'avez pas utilisé la fonction `head()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `head(x = ...)` avec les arguments corrects.")

test_function("sample", args = c("piece", 10, TRUE),
              not_called_msg = "Vous n'avez pas utilisé la fonction `sample()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `sample(x = ..., taille = ..., replace = TRUE)` avec les arguments corrects.")
              
test_function("mean", args = "lancers_10 == Pile",
              not_called_msg = "Vous n'avez pas utilisé la fonction `mean()` !",
              incorrect_msg = "Vous n'avez pas utilisé la fonction `mean(x = ...)` avec les arguments corrects.")

test_object("prop_10")

test_error(incorrect_msg = "Une erreur est présente dans votre code-source.")

success_msg("Bravo ! Il nous reste maintenant à calculer la proportion de pile obtenue pour un nombre variable de lancers.")
```
