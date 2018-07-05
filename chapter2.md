---
  title: "Chapter 2. Basic Linear Regression"
  description: "This chapter considers regression in the case of only one explanatory variable. Despite this seeming simplicity, many deep ideas of regression can be developed in this framework. By limiting ourselves to the one variable case, we can illustrate the relationships between two variables graphically. Graphical tools prove to be important for developing a link between the data and a predictive model."

---
## Correlation

```yaml
type: NormalExercise

xp: 100

key: 053627df3c



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_qlpe86qi&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_w18zht77" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Calculate and interpret a correlation coefficient
- Interpret correlation coefficients by visualizing scatter plots

`@hint`












---
## Correlations and the Wisconsin lottery

```yaml
type: NormalExercise

xp: 100

key: 5e10bb2831



```

The Wisconsin lottery dataset, `Wisc_lottery`,has already been read into a dataframe `Lot`.

Like insurance, lotteries are uncertain events and so the skills to work with and interpret lottery data are readily applicable to insurance. It is common to report sales and population in thousands of units, so this exercise gives you practice in rescaling data via linear transformations.

`@instructions`
- From the available population and sales variables, create new variables in the dataframe `Lot`, `pop_1000` and `sales_1000` that are in thousands (of people and of dollars, respectively).
- Create summary statistics for the dataframe that includes these new variables.
- Plot `pop_1000` versus `sales_1000`.
- Calculate the correlation between `pop_1000` versus `sales_1000` using the function [cor()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/cor). How does this differ between the correlation between population and sales in the original units?

`@hint`
Use the dataframe to refer to pop and sales as `Lot$pop` and `Lot$sales`, respectively

`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
#library(Rcmdr)
#library(psych)
```
`@sample_code`
```{r}
# Create new variables, say, `pop_1000` and `sales_1000`
Lot$pop_1000 <- ___
___ <- Lot$sales/1000

# Create summary statistics for the dataframe
summary(___)

# Plot `pop_1000` versus `sales_1000`.
plot(___, ___)

# Calculate the correlation between `pop_1000` versus `sales_1000` 
cor(___, ___)
```
`@solution`
```{r}
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
summary(Lot)
#(as.data.frame(psych::describe(Lot)))[,c(2,3,4,5,8,9)]
#(as.data.frame(psych::describe(Lot[,c("pop_1000", "sales_1000")])))[,c(2,3,4,5,8,9)]
#Rcmdr::numSummary(Lot[,c("pop_1000", "sales_1000")], statistics = c("mean", "sd", "quantiles"), quantiles = c(0,.5,1))
plot(Lot$pop_1000, Lot$sales_1000)
cor(Lot$pop_1000, Lot$sales_1000)
```
`@sct`
```{r}
success_msg("Congratulations! We will rescale data using 'linear' transformations regularly. In part we do this for communicating our analysis to others. Also in part, this is for our own convenience as it can allow us to see patterns more readily.")
```






---
## Method of least squares

```yaml
type: NormalExercise

xp: 100

key: 8a81e02f41



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_6finvcp7&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_5pgz5f8p" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Fit a line to data using the method of least squares
- Predict an observation using a least squares fitted line

`@hint`












---
## Least squares fit using housing prices

```yaml
type: NormalExercise

xp: 100

key: 6408595f66



```

The prior video analyzed the effect that a zip code's population has on lottery sales. Instead of population, suppose that you wish to understand the effect that housing prices have on the sale of lottery tickets. The dataframe `Lot`, read in from the Wisconsin lottery dataset  `Wisc_lottery`, contains the variable `medhome` which is the median house price for each zip code, in thousands of dollars. In this exercise, you will get a feel for the distribution of this variable by examining summary statistics, examine its relationship with sales graphically and via correlations, fit a basic linear regression model and use this model to predict sales.



`@instructions`
- Summarize the dataframe `Lot` that contains `medhome` and `sales`.
- Plot `medhome` versus `sales`. Summarize this relationship by calculating the corresponding correlation coefficient using the function [cor()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/cor).
- Using the function [lm()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/lm), regress `medhome`, the explanatory variable, on `sales`, the outcome variable. Display the regression coefficients to four significant digits.
- Use the function [predict()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/predict) and the fitted regression model to predict sales assuming that the median house price for a zip code is 50 (in thousands of dollars).

`@hint`


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
# Summarize the dataframe `Lot` that contains `medhome` and `sales`
summary(Lot)
# Plot and calculate the correlation of `medhome` versus `sales`. 
cor(___, ___)
plot(___, ___)

# Regress `medhome`  on `sales`. Display the regression coefficients to four significant digits.
model_blr1 <- lm(___ ~ ___, data = Lot)
round(coefficients(model_blr1), digits= ---)

# Predict sales assuming that the median house price is 50 
newdata <- data.frame(medhome = ___)
predict(model_blr1, newdata)
```
`@solution`
```{r}
#(as.data.frame(psych::describe(Lot[,c("medhome", "sales")])))[,c(2,3,4,5,8,9)]
cor(Lot$medhome,Lot$sales)
plot(Lot$medhome,Lot$sales)
model_blr1 <- lm(sales ~ medhome, data = Lot)
round(coefficients(model_blr1), digits=4)
newdata <- data.frame(medhome = 50)
predict(model_blr1, newdata)
```
`@sct`
```{r}
success_msg("Congratulations! You now have experience fitting a regression line and using this line for predictions, just as Galton did when he used parents' heights to predict the height of an adult child. Well done!")
```






---
## Understanding Variability

```yaml
type: NormalExercise

xp: 100

key: 542f5fb3be



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_a6j1eyc0&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_x5oq2i5k" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Visualize the ANOVA decomposition of variability
- Calculate and interpret $R^2$, the coefficient of determination
- Calculate and interpret $s^2$ the mean square error
- Explain the components of the ANOVA table

`@hint`












---
## Summarizing measures of uncertainty

```yaml
type: NormalExercise

xp: 100

key: 34b677338b



```

In a previous exercise, you developed a regression line to fit the variable `medhome`, the median house price for each zip code, as a predictor of lottery sales. The regression of `medhome` on `sales` has been summarized in the `R` object `model_blr`.

How reliable is the regression line? In this excercise, you will compute some of the standard measures that are used to summarize the goodness of this fit.

`@instructions`
- Summarize the fitted regression model in an ANOVA table.
- Determine the size of the typical residual, $s$.
- Determine the coefficient of determination, $R^2$.  

`@hint`
You might find more details about the function [anova()]()

`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
model_blr <- lm(sales  ~ medhome, data = Lot)

# Summarize the fitted regression model in an ANOVA table.
anova(___)

# Determine the size of the typical residual, $s$.
sqrt(anova(___)$Mean[2])

# Determine the coefficient of determination, $R^2$. 
summary(___)$r.squared
```
`@solution`
```{r}
model_blr <- lm(sales  ~ medhome, data = Lot)
anova(model_blr)
sqrt(anova(model_blr)$Mean[2])
summary(model_blr)$r.squared
```
`@sct`
```{r}
success_msg("Congratulations! It will be helpful if you compare the results of this exercise to the regression of `pop` on `sales` from the prior video. We have seen that `pop` is more highly correlated with `sales` than `medhome`, so we are expecting greater uncertainty in this regression fit.")

```






---
## Effects of linear transforms on measures of uncertainty

```yaml
type: NormalExercise

xp: 100

key: bf6301515f



```

Let us see how rescaling, a linear transformation, affects our measures of uncertainty. As before, the Wisconsin lottery dataset  `Wisc_lottery` has been read into a dataframe `Lot` that also contains `sales_1000`, sales in thousands of dollars, and `pop_1000`, zip code population in thousands. How do measures of uncertainty change when going from the original units to thousands of those units?

`@instructions`
- Run a regression of `pop` on `sales_1000` and summarize this in an ANOVA table.
- For this regression, determine the $s$ and the coefficient of determination, $R^2$.  
- Run a regression of `pop_1000` on `sales_1000` and summarize this in an ANOVA table.
- For this regression, determine the $s$ and the coefficient of determination, $R^2$.  

`@hint`
The residual standard error is also available as `summary(model_blr1)$sigma`. The coefficient of determination is also available as `summary(model_blr1)$r.squared`.

`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
```
`@sample_code`
```{r}
# Run a regression of `pop` on `sales_1000` and summarize this in an ANOVA table.
model_blr1 <- lm(sales_1000  ~ pop, data = Lot)
anova(___)

# Determine the $s$ and the coefficient of determination, $R^2$.  
sqrt(anova(___)$Mean[2])
summary(___)$r.squared

# Run a regression of `pop_1000` on `sales_1000` and summarize this in an ANOVA table.
model_blr2 <- lm(___  ~ ___, data = Lot)
anova(model_blr2)

# Determine the $s$ and the coefficient of determination, $R^2$. 
___
___
```
`@solution`
```{r}
model_blr1 <- lm(sales_1000  ~ pop, data = Lot)
anova(model_blr1)
sqrt(anova(model_blr1)$Mean[2])
summary(model_blr1)$r.squared
model_blr2 <- lm(sales_1000  ~ pop_1000 , data = Lot)
anova(model_blr2)
sqrt(anova(model_blr2)$Mean[2])
summary(model_blr2)$r.squared

```
`@sct`
```{r}
success_msg("Congratulations! In this exercise, you have seen that rescaling does not affect our measures of goodness of fit in any meaningful way. For example, the coefficient of determinations are completely unaffected. This is helpful because we will rescale variables extensively in our search for patterns in the data.")
```






---
## Statistical inference

```yaml
type: NormalExercise

xp: 100

key: 2cf9065e01



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_s9a4jr3s&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_quj4d5r0" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>


`@instructions`
Learning Objectives

In this module, you learn how to:

- Conduct a hypothesis test for a regression coefficient using either a rejection/acceptance procedure or a p-value
- Calculate and interpret a confidence interval for a regression coefficient
- Calculate and interpret a prediction interval at a specific value of a predictor variable

`@hint`












---
## Statistical inference and Wisconsin lottery

```yaml
type: NormalExercise

xp: 100

key: 3ff9e5fec7



```

In a previous exercise, you developed a regression line with the variable `medhome`, the median house price for each zip code, as a predictor of lottery sales. The regression of `medhome` on `sales` has been summarized in the `R` object `model_blr`.
  
This exercise allows you to practice the standard inferential tasks: hypothesis testing, confidence intervals, and prediction.

`@instructions`
- Summarize the regression model and identify the *t*-statistic for testing the importance of the regression coefficient associated with `medhome`.
- Use the function [confint()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/confint) to provide a 95\% confidence interval for the regression coefficient associated with `medhome`.
- Consider a zip code with a median housing price equal to 50 (in thousands of dollars). Use the function [predict()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/predict) to provide a point prediction and a 95\% prediction interval for sales.

`@hint`
Taking a [summary()] of a regression object produces a new objeect. You can use the [str()] structure command to learn more about the new object. Try out a command such as `str(summary(model_blr))`

`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
model_blr1 <- lm(sales ~ medhome, data = Lot)
# Summarize the regression model and identify the $t$-statistic for testing the importance of the regression coefficient associated with `medhome`.
summary(___)
summary(___)$coefficients
summary(___)$coefficients[,3]

# Provide a 95\% confidence interval for the regression coefficient associated with `medhome`.
confint(___, level = ___)


# Provide a point prediction and a 95\% prediction interval for sales.
NewData1 <- data.frame(medhome = 50)
predict(___, NewData1, interval = "prediction", level = ___)
```
`@solution`
```{r}
model_blr1 <- lm(sales ~ medhome, data = Lot)
summary(model_blr1)
summary(model_blr1)$coefficients
summary(model_blr1)$coefficients[,3]
#Rcmdr::Confint(model_blr1, level = .95)
confint(model_blr1, level = .95)
NewData1 <- data.frame(medhome = 50)
predict(model_blr1, NewData1, interval = "prediction", level = .95)
```
`@sct`
```{r}
success_msg("Congratulations! Much of what we learn from a data modeling exercise can be summarized using standard inferential tools: hypothesis testing, confidence intervals, and prediction.")
```






---
## Diagnostics

```yaml
type: NormalExercise

xp: 100

key: 3488299ef2



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_c6l4p07j&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_4rvf8rp1" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Describe how diagnostic checking and residual analysis are used in a statistical analysis
- Describe several model misspecifications commonly encountered in a regression analysis

`@hint`












---
## Assessing outliers in lottery sales

```yaml
type: NormalExercise

xp: 100

key: 63698e9e8e



```

In an earlier video, we made a scatter plot of population versus sales. This plot exhibits an outlier; the point in the upper left-hand side of the plot represents a zip code that includes Kenosha, Wisconsin. Sales for this zip code are unusually high given its population.  

This exercise summarizes the regression fit both with and without this zip code in order to see how robust our results are to the inclusion of this unusual 

`@instructions`
- A basic linear regression fit of population on sales has already been fit in the object `model_blr`. Fit this same model to the data, omiting Kenosha (observation number 9).
- Plot these two least squares fitted lines superimposed on the full data set.
-  What is the effect on the distribution  of residuals by removing this point? Calculate a qq plot with and without Kenosha.

`@hint`


`@pre_exercise_code`
```{r}
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```
`@sample_code`
```{r}
model_blr <-lm(sales ~ pop, data = Lot)
summary(model_blr)
model_Kenosha <- lm(sales ~ pop, data = Lot, subset = -c(9))
summary(model_Kenosha)

plot(Lot$pop, Lot$sales, xlab = "population", ylab = "sales")
text(5000, 24000, "Kenosha")
abline(model_blr, col="blue")
abline(model_Kenosha, col="red")

par(mfrow = c(1, 2))
qqnorm(residuals(model_blr), main = "")
qqline(residuals(model_blr))
qqnorm(residuals(model_Kenosha), main = "")
qqline(residuals(model_Kenosha))
```
`@solution`
```{r}
model_blr <-lm(sales ~ pop, data = Lot)
summary(model_blr)
model_Kenosha <- lm(sales ~ pop, data = Lot, subset = -c(9))
summary(model_Kenosha)

plot(Lot$pop, Lot$sales, xlab = "population", ylab = "sales")
text(5000, 24000, "Kenosha")
abline(model_blr, col="blue")
abline(model_Kenosha, col="red")

par(mfrow = c(1, 2))
qqnorm(residuals(model_blr), main = "")
qqline(residuals(model_blr))
qqnorm(residuals(model_Kenosha), main = "")
qqline(residuals(model_Kenosha))
```
`@sct`
```{r}
success_msg("Excellent! Just because an observation is unusual does not make it bad or noninformative. Kenosha is close to the Illinois border; residents from Illinois probably participate in the Wisconsin lottery thus effectively increasing the potential pool of sales in Kenosha. Although unusual, there is interesting information to be learned from this observation.")
```




