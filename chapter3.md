---
  title: "Chapter 3. Multiple Linear Regression"
  description: "This chapter introduces linear regression in the case of several explanatory variables, known as multiple linear regression (MLR). Many basic linear regression concepts extend directly, including goodness of fit measures such as the coefficient of determination and inference using t-statistics. Multiple linear regression models provide a framework for summarizing highly complex, multivariate data. Because this framework requires only linearity in the parameters, we are able to fit models that are nonlinear functions of the explanatory variables, thus providing a wide scope of potential applications."

---
## Term life data

```yaml
type: NormalExercise

xp: 100

key: abd03a9e50



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_izascs5a&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_cxgam03z" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`


`@hint`












---
## Method of least squares

```yaml
type: NormalExercise

xp: 100

key: 367b347f21



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_9zszyh42&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_0xy78e1p" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:
  
-  Interpret correlation coefficients by visualizing a scatterplot matrix
-  Fit a plane to data using the method of least squares
-  Predict an observation using a least squares fitted plane

`@hint`












---
## Least squares and term life data

```yaml
type: NormalExercise

xp: 100

key: 73d95801a7



```

The prior video introduced the *Survey of Consumer Finances* (SCF) term life data. A subset consisting of only those who purchased term life insurance, has already been read into a dataframe `Term2`.
  
Suppose that you wish to predict the amount of term life insurance that someone will purchase but are uneasy about the `education` variable. The SCF `education` variable is the number of completed years of schooling and so 12 corresponds to completing high school in the US. Your sense is that, for purposes of purchasing life insurance, high school graduates and those that attend college should be treated the same. So, in this exercise, your will create a new variable, `education1`, that is equal to years of education for those with education less than or equal to 12 and is equal to 12 otherwise.

`@instructions`
- Use the [pmin()](https://www.rdocumentation.org/packages/mc2d/versions/0.1-17/topics/pmin) function to create the `education1` variable as part of the `Term2` dataframe.
- Check your work by examining summary statistics for the revised `Term2` dataframe.
- Examine correlations for the revised dataframe.
- Using the method of least squares and the function [lm()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/lm), fit a MLR model using `logface` as the dependent variables and using `education`, `numhh`, and `logincome` as explanatory variables.
- With this fitted model and the function [predict()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/predict), predict the face amount of insurance that someone with income of 40,000, 11 years of education, and 4 people in the household would purchase.

`@hint`
Remember that your prediction is in log dollars so you need to exponentiate it to get the 
results in the original dollar units

`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
#library(Rcmdr)
```
`@sample_code`
```{r}
# Create the `education1` variable as part of the `Term2` dataframe.
Term2$education1 <- pmin(12, Term2$education)

# Check your work by examining summary statistics for the revised `Term2` dataframe.
summary(___)

# Examine correlations for the revised dataframe.
round(cor(___), digits=3)

# Fit a MLR model using `logface` as the dependent variables and using `education`, `numhh`, and `logincome` as explanatory variables.
Term_mlr2 <- lm(logface ~ ___ + numhh + logincome, data = Term2)

# Predict the face amount of insurance that someone with income of 40,000, 11 years of education, and 4 people in the household would purchase.
newdata <- data.frame(logincome = log(40000), education1 = 11, numhh = 4)
exp(predict(___, newdata))
```
`@solution`
```{r}
Term2$education1 <- pmin(12, Term2$education)
summary(Term2)
round(cor(Term2), digits=3)
Term_mlr2 <- lm(logface ~ education1 + numhh + logincome, data = Term2)
newdata <- data.frame(logincome = log(40000), education1 = 11, numhh = 4)
exp(predict(Term_mlr2, newdata))
```
`@sct`
```{r}
test_error()
test_object("Term2", incorrect_msg = "Is the new education variable properly defined using the pmin() function?")
test_object("Term_mlr2", incorrect_msg = "The MLR model is incorrectly specified.")
test_object("newdata", incorrect_msg = "The new data object is incorrectly specified.")
success_msg("Congratulations! You now have experience fitting a regression plane and using this plane for predictions. Prediction is one of the key tasks of 'predictive modeling.' Well done!")
```






---
## Interpreting coefficients as proportional changes

```yaml
type: NormalExercise

xp: 100

key: 9ae485f649



```

In a previous exercise, you fit a MLR model using `logface` as the outcome variable and using `education`, `numhh`, and `logincome` as explanatory variables; the resulting fit is in the object `Term_mlr`. For this fit, the coefficient associated with `education` is 0.2064. We now wish to interpret this regression coefficient.

The typical interpretation of coefficients in a regression model is as a partial slope. That is, for the coefficient $b_1$ associated with $x_1$, we interpret $b_1$ to be amount that the expected outcome changes per unit change in $x_1$, holding the other explanatory variables fixed. 

For the term life example, the units of the outcome are in logarithmic dollars. So, for small values of $b_1$, we can interpret this to be a *proportional* change in dollars.

`@instructions`
- Determine least square fitted values for several selected values of `education`, holding other explantory variables fixed. For this part of the demonstration, we used their mean values.
- Determine the proportional changes. Note the relation between these values from a discrete change approximation to the regression coefficient for `education` equal to 0.2064.

`@hint`


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
Term_mlr <- lm(logface ~ education + numhh + logincome, data = Term2)
#summary(model_mlr)$coefficients[,1]
```
`@sample_code`
```{r}
Term_mlr <- lm(logface ~ education + numhh + logincome, data = Term2)
summary(Term_mlr)$coefficients[,1]

# Determine least square fitted values for several selected values of `education`, holding other explantory variables fixed.
educ_predict <- c(14,14.1,14.2,14.3)
newdata1 <- data.frame(logincome = mean(Term2$logincome), education = educ_predict, numhh = mean(Term2$numhh))
lsfits1 <- predict(Term_mlr, newdata1)
lsfits1

# Determine the proportional changes. Note the relation between these values from a discrete change approximation to the regression coefficient for `education` equal to 0.2064.
lsfits1[2:4] - lsfits1[1:3]
pchange_fits1 <- exp(lsfits1[2:4] - lsfits1[1:3])
pchange_fits1

```
`@solution`
```{r}
educ_predict <- c(14,14.1,14.2,14.3)
newdata1 <- data.frame(logincome = mean(Term2$logincome), education = educ_predict, numhh = mean(Term2$numhh))
lsfits1 <- predict(Term_mlr, newdata1)
lsfits1
lsfits1[2:4] - lsfits1[1:3]
pchange_fits1 <- exp(lsfits1[2:4] - lsfits1[1:3])
pchange_fits1
```
`@sct`
```{r}
test_error()
test_object("educ_predict", incorrect_msg = "Check to see that values of the education predictor variable are properly coded.")
test_object("newdata1", incorrect_msg = "The new data object is incorrectly specified.")
test_object("lsfits1", incorrect_msg = "The predicted fits at different values of education are incorrectly specified.")
test_object("pchange_fits1", incorrect_msg = "The proportional changes at different values of education are incorrectly specified.")
success_msg("Congratulations! From calculus, small changes in logarithmic values can be interpreted as proportional changes. This is the reason for using natural logarithms.")
```






---
## Interpreting coefficients as elasticities

```yaml
type: NormalExercise

xp: 100

key: 0412663e7b



```

In a previous exercise, you fit a MLR model using `logface` as the outcome variable and using `education`, `numhh`, and `logincome` as explanatory variables; the resulting fit is in the object `Term_mlr`. From this fit, the coefficient associated with `logincome` is 0.4935. We now wish to interpret this regression coefficient. 

The typical interpretation of coefficients in a regression model is as a partial slope. When both $x_1$ and $y$ are in logarithmic units, then we can interpret $b_1$ to be ratio of two percentage changes, known as an *elasticity* in economics. Mathematically, we summarize this as
$$
\frac{\partial \ln y}{\partial \ln x} = \left(\frac{\partial y}{y}\right) ~/ ~\left(\frac{\partial x}{x}\right) .
$$

`@instructions`
- For several selected values of `logincome`, determine the corresponding proportional changes.
- Determine least square fitted values for several selected values of `logincome`, holding other explantory variables fixed.
- Determine the corresponding proportional changes for the fitted values. 
- Calculate the ratio of proportional changes of fitted values to those for income. Note the relation between these values (from a discrete change approximation) to the regression coefficient for `logincome` equal to 0.4935.

`@hint`
When you calculate the ratio of proportional changes of fitted values to those for income, note the relation between these values (from a discrete change approximation) to the regression coefficient for `logincome` equal to 0.4935.

`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
Term_mlr <- lm(logface ~ education + numhh + logincome, data = Term2)
```
`@sample_code`
```{r}
Term_mlr <- lm(logface ~ education + numhh + logincome, data = Term2)
summary(Term_mlr)$coefficients[,1]
# For several selected values of `logincome`, determine the corresponding proportional changes.
logincome_pred <- c(11,11.1,11.2,11.3)
pchange_income <- 100*(exp(logincome_pred[2:4])/exp(logincome_pred[1:3])-1)
pchange_income

# Determine least square fitted values for several selected values of `logincome`, holding other explantory variables fixed.
newdata2 <- data.frame(logincome = logincome_pred, education = mean(Term2$education), numhh = mean(Term2$numhh))
lsfits2 <- predict(Term_mlr, newdata2)

# Determine the corresponding proportional changes for the fitted values. 
pchange_fits2 <- 100*(exp(lsfits2[2:4])/exp(lsfits2[1:3])-1)
pchange_fits2

# Calculate the ratio of proportional changes of fitted values to those for income.
pchange_fits2/pchange_income

```
`@solution`
```{r}
logincome_pred <- c(11,11.1,11.2,11.3)
pchange_income <- 100*(exp(logincome_pred[2:4])/exp(logincome_pred[1:3])-1)
pchange_income
newdata2 <- data.frame(logincome = logincome_pred, education = mean(Term2$education), numhh = mean(Term2$numhh))
lsfits2 <- predict(Term_mlr, newdata2)
pchange_fits2 <- 100*(exp(lsfits2[2:4])/exp(lsfits2[1:3])-1)
pchange_fits2
pchange_fits2/pchange_income
```
`@sct`
```{r}
test_error()
test_object("logincome_pred", incorrect_msg = "Check to see that values of the logarithmic income predictor variable are properly coded.")
test_object("pchange_income", incorrect_msg = "Check to see that the proportional changes of logarithmic income predictor variable are properly coded.")
test_object("newdata2", incorrect_msg = "The new data object is incorrectly specified.")
test_object("lsfits2", incorrect_msg = "The predicted fits at different values of logarithmic income are incorrectly specified.")
test_object("pchange_fits2", incorrect_msg = "The proportional changes at different values of logarithmic income are incorrectly specified.")
success_msg("Congratulations! When both $x_1$ and $y$ are in logarithmic units, then we can interpret $b_1$ to be ratio of two percentage changes, known as an *elasticity* in economics.")
```






---
## Statistical inference and multiple linear regression

```yaml
type: NormalExercise

xp: 100

key: 6d5b099390



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_n9542z90&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_1rrbi7qd" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:
  
-  Explain mean square error and residual standard error in terms of degrees of freedom
-  Develop an ANOVA table and use it to derive the coefficient of determination
-  Calculate and interpret the coefficient of determination adjusted for degrees of freedom
-  Conduct a test of a regression coefficient
-  Summarize regression coefficients using point and interval estimators

`@hint`












---
## Statistical inference and term life

```yaml
type: NormalExercise

xp: 100

key: 5ea0bad4ec



```

In later chapters, we will learn how to specify a model using diagnostics techniques; these techniques were used to specify face in log dollars for the outcome and similarly income in log dollars as an explanatory variable. Just to see how things work, in this exercise we will create new variables `face` and `income` that are in the original units and run a regression with these. We have already seen that rescaling by constants do not affect relationships but can be helpful with interpretations, so we define both  `face` and `income` to be in thousands of dollars. A prior video introduced the term life dataframe `Term2`.


`@instructions`
- Create `Term2$face` by exponentiating `logface` and dividing by 1000. For convenience, we are storing this variable in the data set `Term2`. Use the same process to create `Term2$income`.
- Run a regression using `face` as the outcome variable and `education`, `numhh`, and `income` as explanatory variables.
- Summarize this model and identify the residual standard error ($s$) as well as the coefficient of determination ($R^2$) and the version adjusted for degrees of freedom ($R_a^2$).

`@hint`


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
```
`@sample_code`
```{r}
# Create `Term2$face` and  `Term2$income`
Term2$face <- exp(___)/___
Term2$income <- exp(___)/___

# Run a regression using `face` as the outcome variable and `education`, `numhh`, and `income` as explanatory variables.
Term_mlr1 <- lm(face ~ ___, data = Term2)

# Summarize this model
summary(Term_mlr1)
```
`@solution`
```{r}
Term2$face <- exp(Term2$logface)/1000
Term2$income <- exp(Term2$logincome)/1000
Term_mlr1 <- lm(face ~ education + numhh + income, data = Term2)
summary(Term_mlr1)
```
`@sct`
```{r}
success_msg("Congratulations! Compare these goodness of fit measures to those where income and face are in logarithmic units. Although not the only indicators, you will see that the proportion of variability explained (R square) and the statistical significance of coefficients are strikingly higher in the model with variables in logged units.")
```






---
## Binary variables

```yaml
type: NormalExercise

xp: 100

key: b765c6a8c0



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_jfmz8kg0&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_qxygjiq2" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:
  
- Interpret regression coefficients associated with binary variables
- Use binary variables and interaction terms to create regression models that are nonlinear in the covariates

`@hint`












---
## Binary variables and term life

```yaml
type: NormalExercise

xp: 100

key: aead731b59



```

In the prior video, we saw how the variable `single` can be used with logarithmic income to explain logarithmic face amounts of term life insurance that people purchase. The coefficient associated with this variable turns out to be negative which is intuitively appealing; if an individual is single, then that person may not have the strong need to purchase financial security for others in the event of unexpected death. 

In this exercise, we will extend this by incorporating `single` into our larger regression model that contains other explanatory varibles, `logincome`, `education` and `numhh`. The data have been pre-loaded into the dataframe `Term4`. 

`@instructions`
- Calculate a table of correlation coefficients to examine pairwise linear relationships among the variables `numhh`, `education`, `logincome`, `single`, and  `logface`.
- Fit a MLR model of `logface` using explanatory variables `numhh`, `education`, `logincome`, and `single`. Examine the residual standard deviation $s$, the coefficient of determination $R^2$, and the adjusted version $R_a^2$. Also note the statistical significance of the coefficient associated with `single`.
- Repeat the MLR model fit while adding the interaction term  `single*logincome`.

`@hint`


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term4 <- Term1[,c("numhh", "education", "logincome", "marstat", "logface")]
Term4$single <- 1*(Term4$marstat == 0)
```
`@sample_code`
```{r}
# Calculate a table of correlation coefficients
round(___(Term4[,c("numhh", "education", "logincome", "single", "logface")]), digits = 3)

# Fit a MLR model of `logface` using explanatory variables `numhh`, `education`, `logincome`, and `single`.
Term_mlr3 <- lm(logface ~ education + numhh + logincome + single, data = Term4)
summary(Term_mlr3)

# Repeat the MLR model fit while adding the interaction term  `single*logincome`.
Term_mlr4 <- lm(logface ~ education + numhh + logincome + single + single*logincome, data = Term4)
summary(Term_mlr4)
```
`@solution`
```{r}
round(cor(Term4[,c("numhh", "education", "logincome", "single", "logface")]), digits = 3)
Term_mlr3 <- lm(logface ~ education + numhh + logincome + single, data = Term4)
summary(Term_mlr3)
Term_mlr4 <- lm(logface ~ education + numhh + logincome + single + single*logincome, data = Term4)
summary(Term_mlr4)
```
`@sct`
```{r}
success_msg("Congratulations! From a correlation table, you saw that there are relationships with among explanatory variables and so it is not clear whether adding `single` to the model would be helpful. You explored this by first fitting a model by just adding the binary variable single, examined summary statistics, and checked the significance of the variable. Then, you explored the utility of the interaction of `single` with logarithmic income. Well done!")
```






---
## Categorical variables

```yaml
type: NormalExercise

xp: 100

key: 33c5fa4b6f



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_gkywbwai&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_n73q1ka4" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:
  
- Represent categorical variables using a set of binary variables
- Interpret the regression coefficients associated with categorical variables
- Describe the effect of the reference level choice on the model fit

`@hint`












---
## Categorical variables and Wisconsin hospital costs

```yaml
type: NormalExercise

xp: 100

key: 6109c06795



```

This exercise examines the impact of various predictors on hospital charges. Identifying predictors of hospital charges can provide direction for hospitals, government, insurers and consumers in controlling these variables that in turn leads to better control of hospital costs. The data, from 1989, are aggregated by: 

- `drg`, diagnostic related groups of costs, 
- `payer`, type of health care provider (Fee for service, HMO, and other), and 
- `hsa`, nine major geographic areas in Wisconsin.

Some preliminary analysis of the data has already been done. In this exercise, we will analyze `logcharge`, the logarithm of total hospital charges per number of discharges, in terms of `log_numdschg`, the logarithm of the number of discharges. In the dataframe `Hcost` which has been loaded in advance, we restrict consideration to three types of drgs, numbers 209, 391, and 431.

`@instructions`
- Fit a basic linear regression model using logarithmic number of discharges to predict logarithmic hospital costs and superimposed the fitted regression line on the scatter plot.
- Produce a scatter plot of logarithmic number of discharges to predict logarithmic hospital costs. Allow plotting symbols and colors to vary by diagnostic related group.
- Fit a MLR model using logarithmic number of discharges to predict logarithmic hospital costs, allowing intercepts and slopes to vary by diagnostic related groups.
- Superimpose the fits from the MLR model on the scatter plot of logarithmic number of discharges to predict logarithmic hospital costs.

`@hint`


`@pre_exercise_code`
```{r}
Hcost <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/2cc1e2739bf827093db31d7c4e6dcdc348ac984e/WiscHcosts.csv", header = TRUE)
Hcost1 <- subset(Hcost, drg == 209|drg == 391|drg == 430)
```
`@sample_code`
```{r}
# Fit a basic linear regression model using logarithmic number of discharges to predict logarithmic hospital costs and superimposed the fitted regression line on the scatter plot.
hosp_blr <- lm(logcharge~log_numdschg, data=Hcost1)
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge")
abline(hosp_blr, col="red")

# Produce a scatter plot of logarithmic number of discharges to predict logarithmic hospital costs. Allow plotting symbols and colors to vary by diagnostic related group.
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
    pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
legend("left", legend=c("drg 209","drg 391", "drg 430"), col=c("red", "black", "blue"), pch = c(1,2,3))

# Fit a MLR model allowing intercepts and slopes to vary by drg.
hosp_mlr <- lm(logcharge~log_numdschg + as.factor(drg)*log_numdschg, data=Hcost1)

# Superimpose the fits from the MLR model on the scatter plot of logarithmic number of discharges to predict logarithmic hospital costs.
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
         pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
xseq <- seq(0,10,length.out=100)
coef <- summary(hosp_mlr)$coefficients[,1]
fit209 <- coef[1] + coef[2]*xseq
lines(xseq,fit209, col="red")
fit391 <- coef[1] + coef[3] + (coef[2] + coef[5])*xseq
lines(xseq,fit391, col="black")
fit430 <- coef[1] + coef[4] + (coef[2] + coef[6])*xseq
lines(xseq,fit430, col="blue")
```
`@solution`
```{r}
hosp_blr <- lm(logcharge~log_numdschg, data=Hcost1)
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge")
abline(hosp_blr, col="red")

plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
    pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
legend("left", legend=c("drg 209","drg 391", "drg 430"), col=c("red", "black", "blue"), pch = c(1,2,3))

hosp_mlr <- lm(logcharge~log_numdschg + as.factor(drg)*log_numdschg, data=Hcost1)
#summary(hosp_mlr)$coefficients[,1]
plot(logcharge~log_numdschg, data=Hcost1, xlab = "log number discharges", ylab = "log charge",
         pch= as.numeric(as.factor(Hcost1$drg)), 
    col = c("red", "black", "blue")[as.factor(Hcost1$drg)])
xseq <- seq(0,10,length.out=100)
coef <- summary(hosp_mlr)$coefficients[,1]
fit209 <- coef[1] + coef[2]*xseq
lines(xseq,fit209, col="red")
fit391 <- coef[1] + coef[3] + (coef[2] + coef[5])*xseq
lines(xseq,fit391, col="black")
fit430 <- coef[1] + coef[4] + (coef[2] + coef[6])*xseq
lines(xseq,fit430, col="blue")
```
`@sct`
```{r}
success_msg("Congratulations! When you superimposed the fits from the MLR model on the scatter plot of logarithmic number of discharges to predict logarithmic hospital costs, note how slopes differ dramatically from the slope from the basic linear regression model.")
```






---
## Hypothesis testing

```yaml
type: NormalExercise

xp: 100

key: 1ce81a782c



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_gs9oqymi&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_j9btj8ns" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>


`@instructions`
Learning Objectives

In this module, you learn how to:

-  Jointly test the significance of a set of regression coefficients using the general linear hypothesis
-  Conduct a test of a regression coefficient versus one- or two-side alternatives

`@hint`












---
## Hypothesis testing and term life

```yaml
type: NormalExercise

xp: 100

key: 1d698fbe58



```

With our `Term life` data, let us compare a model based on the binary variable that indicates whether a survey respondent is single versus the more complex marital status, `marstat`. In principle, more detailed information is better. But, it may be that the additional information in `marstat`, compared to `single`, does not help fit the data in a significantly better way. 

As part of the preparatory work, the dataframe `Term4` is available that includes the binary variable `single` and the factor `marstat`. Moreover, the regression object `Term_mlr` contains information in a multiple linear regression fit of `logface` on the base explanatory variables 'logincome`, `education`, and `numhh`. 

`@instructions`
- Fit a MLR model using the base explanatory variables plus `single` and another model using the base variables plus `marstat`.
- Use the F test to decide whether the additional complexity `marstat` is warranted by calculating the p-value associated with this test.
- Fit a MLR model using the base explanatory variables plus `single` interacted with `logincome` and another model using the base variables plus `marstat` interacted with `logincome`.
- Use the F test to decide whether the additional complexity `marstat` is warranted by calculating the p-value associated with this test.

`@hint`
Here is the code to calculate it by hand
Fstat12 <- (anova(Term_mlr1)$`Sum Sq`[5] - 
              anova(Term_mlr2)$`Sum Sq`[5])/(1*anova(Term_mlr2)$`Mean Sq`[5])
Fstat12
cat("p-value is", 1 - pf(Fstat12, df1 = 1 , df2 = anova(Term_mlr2)$Df[5]))

`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term4 <- Term1[,c("numhh", "education", "logincome", "marstat", "logface")]
Term4$single <- 1*(Term4$marstat == 0)
Term4$marstat <- as.factor(Term4$marstat)
Term_mlr <- lm(logface ~ logincome + education + numhh , data = Term4)
anova(Term_mlr)
```
`@sample_code`
```{r}
# Fit a MLR model using the base explanatory variables plus `single` and another model using the base variables plus `marstat`.
Term_mlr1 <- lm(logface ~ logincome + education + numhh +single, data = Term4)
Term_mlr2 <- lm(logface ~ logincome + education + numhh +marstat, data = Term4)

# Use the F test to decide whether the additional complexity `marstat` is warranted by calculating the p-value associated with this test.
anova(Term_mlr1,Term_mlr2)

# Fit a MLR model using the base explanatory variables plus `single` interacted with `logincome` and another model using the base variables plus `marstat` interacted with `logincome`.
Term_mlr3 <- lm(logface ~ logincome + education + numhh + single*logincome, data = Term4)
Term_mlr4 <- lm(logface ~ logincome + education + numhh +marstat*logincome, data = Term4)

# Use the F test to decide whether the additional complexity `marstat` is warranted by calculating the p-value associated with this test.
anova(Term_mlr3,Term_mlr4)
```
`@solution`
```{r}
Term_mlr1 <- lm(logface ~ logincome + education + numhh +single, data = Term4)
Term_mlr2 <- lm(logface ~ logincome + education + numhh +marstat, data = Term4)
anova(Term_mlr1,Term_mlr2)
#Fstat12 <- (anova(Term_mlr1)$`Sum Sq`[5] - 
#              anova(Term_mlr2)$`Sum Sq`[5])/(1*anova(Term_mlr2)$`Mean Sq`[5])
#Fstat12
#cat("p-value is", 1 - pf(Fstat12, df1 = 1 , df2 = anova(Term_mlr2)$Df[5]))
Term_mlr3 <- lm(logface ~ logincome + education + numhh + single*logincome, data = Term4)
Term_mlr4 <- lm(logface ~ logincome + education + numhh +marstat*logincome, data = Term4)
anova(Term_mlr3,Term_mlr4)
```
`@sct`
```{r}
success_msg("Congratulations! Hypothesis testing is a primary tool for  'inferring' about the real world {in contrast to mathematical 'deduction'.} Moreover, as we will see in the next chapter, it can also be used to develop a model.")
```






---
## Hypothesis testing and Wisconsin hospital costs

```yaml
type: NormalExercise

xp: 100

key: 4431c6edd1



```

In a previous exercise, you were introduced to a dataset with hospital charges aggregated by:

- `drg`, diagnostic related groups of costs, 
- `payer`, type of health care provider (Fee for service, HMO, and other), and 
- `hsa`, nine major geographic areas.

We continue our analysis of the outcome variable  `logcharge`, the logarithm of total hospital charges per number of discharges, in terms of `log_numdschg`, the logarithm of the number of discharges, as well as the three categorical variables used in the aggregation. As before, we restrict consideration to three types of drgs, numbers 209, 391, and 431 that has been preloaded in the dataframe `Hcost1`.

`@instructions`
- Fit a basic linear regression model using logarithmic hospital costs as the outcome variable and explanatory variable logarithmic number of discharges.
- Fit a MLR model using logarithmic hospital costs as the outcome variable and explanatory variables logarithmic number of discharges and the categorical variable diagnostic related group. Identify the *F* statistic and *p* value that test the importance of diagnostic related group. 
- Fit a MLR model using logarithmic hospital costs as the outcome variable and explanatory variable logarithmic number of discharges interacted with diagnostic related group. Identify the *F* statistic and *p* value that test the importance of diagnostic related group interaction with logarithmic number of discharges.
- Calculate a coefficient of determination, $R^2$, for each of these models as well as for a model using logarithmic number of discharges and categorical variable `hsa` as predictors.

`@hint`


`@pre_exercise_code`
```{r}
Hcost <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/2cc1e2739bf827093db31d7c4e6dcdc348ac984e/WiscHcosts.csv", header = TRUE)
Hcost1 <- subset(Hcost, drg == 209|drg == 391|drg == 430)
```
`@sample_code`
```{r}
# Regress log charges on log number of discharges
hosp_blr <- lm(logcharge ~ log_numdschg , data=Hcost1)
anova(hosp_blr)

# Regress log charges on log number of discharges and drg. Identify the *F* statistic and *p* value that test the importance of diagnostic related group.
hosp_mlr1 <- lm(logcharge ~ log_numdschg + as.factor(drg), data=Hcost1)
anova(hosp_mlr1)

# Regress log charges on the interaction of log number of discharges and drg. 
hosp_mlr2 <- lm(logcharge ~ log_numdschg + as.factor(drg)*log_numdschg, data=Hcost1)
anova(hosp_mlr2)

# Calculate a coefficient of determination, $R^2$, for each of these models as well as for a model using logarithmic number of discharges and categorical variable `hsa` as predictors.
summary(hosp_blr)$r.squared
summary(hosp_mlr1)$r.squared
summary(hosp_mlr2)$r.squared

hosp_mlr3 <- lm(logcharge ~ log_numdschg + as.factor(hsa)*log_numdschg, data=Hcost1)
summary(hosp_mlr3)$r.squared
```
`@solution`
```{r}

```
`@sct`
```{r}
success_msg("Congratulations! By examining the coefficients of determination, $R^2$, for each of these models, you see that this provides one piece of evidence that the `hsa` is a far poorer predictor of costs than `drg`.")
```




