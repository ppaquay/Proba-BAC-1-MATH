---
title       : Distributions de probabilités discrètes
description : Nous allons dans ce chapitre explorer les concepts basiques du calcul des probabilités.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## A really bad movie

```yaml
type: MultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: f6b66ff00c
```

Have a look at the plot that showed up in the viewer to the right. Which type of movie has the worst rating assigned to it?

`@instructions`
- Adventure
- Action
- Animation
- Comedy

`@hint`
Have a look at the plot. Which color does the point with the lowest rating have?

`@pre_exercise_code`
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

library(ggplot2)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

---
## Le lancer d'une pièce de monnaie

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: c58587436b
```

Nous avons vu que si un évènement $E$ a une probabilité $p$ de se produire, il semble naturel lorsque l'expérience aléatoire est répétée un grand nombre de fois, que la fraction du temps où $E$ va se réaliser sera approximativement égale à $p$.

Par exemple, lors du lancer d'une pièce de monnaie bien équilibrée, nous nous attendons à ce que la probabilité d'obtenir pile soit de 1/2. D'après le raisonnement évoqué ci-dessus, si nous lancions une pièce de monnaie un grand nombre de fois, nous devrions voir que la fraction du temps où pile apparaît est égale à 1/2.

Nous allons simuler ce phénomène aléatoire et examiner les résultats obtenus.


`@instructions`
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

`@hint`
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

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
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

`@solution`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
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
