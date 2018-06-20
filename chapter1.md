---
title: "Chapter 1. Regression and the Normal Distribution"
description: "Regression analysis is a statistical method that is widely used in many fields of study, with actuarial science being no exception. This chapter introduces the role of the normal distribution in regression and the use of logarithmic transformations in specifying regression relationships."



---
## Fitting a normal distribution

```yaml
type: NormalExercise
key: 816f45ca82
lang: r
xp: 100
skills: 1
```

See the video on Fitting a normal distribution

(<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_e885sczm&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_tnia11ze" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>)

---
## Fitting Galton's height data

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 210d9bb371
```

The Galton data has already been read into a dataset called `heights`. These data include the heights of 928 adult children `child_ht`, together with an index of their parents' height `parent_ht`.  The video explored the distribution of the parents' height; in this assignment, we investigate the distribution of the heights of the adult children.

`@instructions`
-  Define the height of an adult child as a local variable
-  Use the function [mean()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/mean/) to calculate the mean and the function [sd()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/sd/) to calculate the standard deviation 
-  Use the normal approximation and the function [pnorm()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/Normal/)  determine the probability that a child's height is less than 72 inches

`@hint`
Remember that we can reference a variable, say `var`, from a data set such as `heights`, as `heights$var`.

`@pre_exercise_code`
```{r}
heights <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/c85ede6c205d22049e766bd08956b225c576255b/galton_height.csv", header = TRUE)
```
`@sample_code`
```{r}
#Define the variable
ht_child <- ___

#Calculate the mean height
mchild <- ___
mchild

#Calculate the standard deviation of heights
sdchild <- ___
sdchild

#Determine the probability that a child's height is less than 72 inches
___(72, mean=mchild, sd=sdchild)
```
`@solution`
```{r}
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
pnorm(72,mean=mchild, sd=sdchild)
```
`@sct`
```{r}
test_error()
test_object("ht_child", incorrect_msg = "The child's height variable was defined in the wrong way. (You might check the hint.)")
success_msg("Excellent! With this procedure, you can now calculate probabilities for any distribution using a normal curve approximation.")
```





---
## Visualizing child's height distribution

```yaml
type: NormalExercise
key: 0be3d7b94d
lang: r
xp: 100
skills: 1
```


As in the prior exercise, from the Galton dataset `heights`, the heights of 928 adult children have been used to create a local variable called `ht_child`. We also have basic summary statistics, the mean height `mchild` and the standard deviation of heights in `sdchild`. In this exercise, we explore the fit of the normal curve to this distribution.

`@instructions`
-  To visualize the distribution, use the function [hist()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist/) to calculate the histogram. Use the `freq = FALSE` option to give a histogram with proportions instead of counts.
-  Use the function [seq()](https://www.rdocumentation.org/packages/base/versions/3.5.0/topics/seq) to determine a sequence that can be used for plotting. Then, function [lines()](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/lines/) to superimpose a normal curve on the histogram
-  Determine the probability that a son's height is greater than 72 inches

`@hint`
No hints for now. No hints for now. No hints for now.

`@pre_exercise_code`
```{r}
heights <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/c85ede6c205d22049e766bd08956b225c576255b/galton_height.csv", header = TRUE)
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
```
`@sample_code`
```{r}
#Visualize the Distribution
___(___, freq = FALSE)

#Determine a sequence. Then, graph a histogram with a normal curve superimposed
x <- seq(60, 80,by = 0.1)
___(x, dnorm(x,mean = mchild, sd = sdchild), col = "blue")

# Determine the probability that a son's height is greater than 60 inches
1 - pnorm__
```
`@solution`
```{r}
hist(ht_child, freq = FALSE)
x <- seq(60, 80,by = 0.1)
lines(x, dnorm(x,mean = mchild, sd = sdchild), col = "blue")
1 - pnorm(72, mean = mchild , sd = sdchild)
```
`@sct`
```{r}
success_msg("Excellent! Visualizing the distribution, especially with reference to a normal, is important for communicating results of your analysis.")
```

