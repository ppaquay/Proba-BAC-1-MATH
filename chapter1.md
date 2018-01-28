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

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("https://s3.amazonaws.com/assets.datacamp.com/course/teach/movies.RData"))
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"), c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

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

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
