---
  title: "Chapter 4. Variable Selection"
  description: "This chapter describes tools and techniques to help you select variables to enter into a linear regression model, beginning with an iterative model selection process. In applications with many potential explanatory variables, automatic variable selection procedures are available that will help you quickly evaluate many models. Nonetheless, automatic procedures have serious limitations including the inability to account properly for nonlinearities such as the impact of unusual points; this chapter expands upon the Chapter 2 discussion of unusual points. It also describes collinearity, a common feature of regression data where explanatory variables are linearly related to one another. Other topics that impact variable selection, including out-of-sample validation, are also introduced."

---
## An iterative approach to data analysis and modeling

```yaml
type: NormalExercise

xp: 100

key: 619dd067ca



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_53yv68dd&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_yxfgvaql" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>


`@instructions`
Learning Objectives

In this module, you learn how to:
  
-  Describe the iterative approach to data analysis and modeling.

`@hint`












---
## Insert exercise title here

```yaml
type: MultipleChoiceExercise

xp: 50

key: 6454b41b18



```

Which of the following is not true?

`@instructions`
- A. Diagnostic checking reveals symptoms of mistakes made in previous specifications.
- B. Diagnostic checking provides ways to correct mistakes made in previous specifications.
- C. Model formulation is accomplished by using prior knowledge of relationships.
- [D. Understanding theoretical model properties is not really helpful when matching a model to data or inferring general relationships based on the data.]

`@hint`












---
## Automatic variable selection procedures

```yaml
type: NormalExercise

xp: 100

key: 822c16b451



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_94bk7tyn&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_vq3apay6" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:
  
- Identify some examples of automatic variable selection procedures
- Describe the purpose of automatic variable selection procedures and their limitations
- Describe "data-snooping"

`@hint`












---
## Data-snooping in stepwise regression

```yaml
type: NormalExercise

xp: 100

key: 33d706f7cb



```

Automatic variable selection procedures, such as the classic stepwise regression algorithm, are very good at detecting patterns. Sometimes they are too good in the sense that they detect patterns in the sample that are not evident in the population from which the data are drawn. The detect "spurious" patterns.

This exercise illustrates this phenomenom by using a simulation, designed so that the outcome variable (*y*) and the explanatory variables are mutually independent. So, by design, there is no relationship between the outcome and the explanatory variables.

As part of the code set-up, we have *n* = 100 observations generated of the outcome *y* and 50 explanatory variables, `xvar1` through `xvar50`. As anticipated, collections of explanatory variables are not statistically significant. However, with the [step()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/step) function, you will find some statistically significant relationships!

`@instructions`
- Fit a basic linear regression model and MLR model with the first ten explanatory variables. Compare the models via an *F* test.
- Fit a multiple linear regression model with all fifty explanatory variables. Compare this model to the one with ten variables via an *F* test.
- Use the `step` function to find the best model starting with the fitted model containing all fifty explanatory variables and summarize the fit. 

`@hint`
The code shows stepwise regression using BIC, a criterion that results in simpler models than AIC. For AIC, use the option `k=2` in the [step()] function (the default)


`@pre_exercise_code`
```{r}
set.seed(1237)
X <- as.data.frame(matrix(rnorm(100*50, mean = 0, sd = 1), ncol = 50))
colnames(X) <- paste("xvar", 1:50, sep = "")
X$y <- with(X, matrix(rnorm(100*1, mean = 0, sd = 1), ncol = 1))
```
`@sample_code`
```{r}
# Fit a basic linear regression model and MLR model with the first ten explanatory variables. Compare the models via an *F* test.
model_step1 <- lm(y ~ xvar1, data = X)
model_step10 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10, data = X)
anova(___, ___)

# Fit a multiple linear regression model with all fifty explanatory variables. Compare this model to the one with ten variables via an *F* test.
model_step50 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10 + xvar11 + xvar12 + xvar13 + xvar14 + xvar15 + xvar16 + xvar17 + xvar18 + xvar19 + xvar20 + xvar21 + xvar22 + xvar23 + xvar24 + xvar25 + xvar26 + xvar27 + xvar28 + xvar29 + xvar30 + xvar31 + xvar32 + xvar33 + xvar34 + xvar35 + xvar36 + xvar37 + xvar38 + xvar39 + xvar40 + xvar41 + xvar42 + xvar43 + xvar44 + xvar45 + xvar46 + xvar47 + xvar48 + xvar49 + xvar50, data = X)
anova(___, ___)

# Use the `step` function, starting with the fitted model containing all fifty explanatory variables and summarize the fit.
#For BIC: 
model_stepwise <- step(___, data = X, direction= "both", k = log(nrow(X)), trace = 0) 
summary(model_stepwise)
```

`@solution`
```{r}
model_step1 <- lm(y ~ xvar1, data = X)
model_step10 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10, data = X)
anova(model_step1,model_step10)
model_step50 <- lm(y ~ xvar1 + xvar2 + xvar3 + xvar4 + xvar5 + xvar6 + xvar7 + xvar8 + xvar9 + xvar10 + xvar11 + xvar12 + xvar13 + xvar14 + xvar15 + xvar16 + xvar17 + xvar18 + xvar19 + xvar20 + xvar21 + xvar22 + xvar23 + xvar24 + xvar25 + xvar26 + xvar27 + xvar28 + xvar29 + xvar30 + xvar31 + xvar32 + xvar33 + xvar34 + xvar35 + xvar36 + xvar37 + xvar38 + xvar39 + xvar40 + xvar41 + xvar42 + xvar43 + xvar44 + xvar45 + xvar46 + xvar47 + xvar48 + xvar49 + xvar50, data = X)
anova(model_step10,model_step50)

#For BIC: 
model_stepwise <- step(model_step50, data = X, direction= "both", k = log(nrow(X)), trace = 0) 
summary(model_stepwise)
```

`@sct`
```{r}
success_msg("Excellent! The step procedure repeatedly fits many models to a data set. We summarize each fit with hypothesis testing statistics like t-statistics and p-values. But, remember that hypothesis tests are designed to falsely detect a relationship a fraction of the time (typically 5%). For example, if you run a t-test 50 times (for each explanatory variable), you can expect to get two or three statistically significant explanatory variables even for unrelated variables (because 50 times 0.05 = 2.5).")
```






---
## Residual analysis

```yaml
type: NormalExercise

xp: 100

key: 57e7e1e321



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_bwhmsm8k&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_zvacn361" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>


`@instructions`
Learning Objectives

In this module, you learn how to:

- Explain how residual analysis can be used to improve a model specification
- Use relationships between residuals and potential explanatory variables to improve model specification

`@hint`












---
## Residual analysis and risk manager survey

```yaml
type: NormalExercise

xp: 100

key: 953793c347



```

This exercise examines data, pre-loaded in the dataframe `survey`, from a survey on the cost effectiveness of risk management practices. Risk management practices are activities undertaken by a firm to minimize the potential cost of future losses, such as the event of a fire in a warehouse or an accident that injures employees. This exercise develops a model that can be used to make statements about cost of managing risks.

A measure of risk management cost effectiveness, `logcost`, is the outcome variable. This variable is defined as total property and casualty premiums and uninsured losses as a proportion of total assets, in logarithmic units. It is a proxy for annual expenditures associated with insurable events, standardized by company size. Explanatory variables include
`logsize`, the logarithm of total firm assets, and `indcost`, a measure of the firm's industry risk.

`@instructions`
- Fit and summarize a MLR model using `logcost` as the outcome variable and `logsize` and `indcost` as explanatory variables.
- Plot residuals of the fitted model versus `indcost` and superimpose a locally fitted line using the `R` function [lowess()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/lowess).
- Fit and summarize a MLR model of `logcost` on `logsize`, `indcost` and a squared version of `indcost`.
- Plot residuals of the fitted model versus `indcost' and superimpose a locally fitted line using [lowess()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/lowess).

`@hint`
You can access model residuals using `mlr.survey1$residuals` or `mlr.survey1($residuals)`

`@pre_exercise_code`
```{r}
survey <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/dc1c5bce43ef076aa77169a242118e2e58d01f82/Risk_survey.csv", header=TRUE)
survey$logcost <- log(survey$firmcost)
```
`@sample_code`
```{r}
# Regress `logcost` on `logsize` and `indcost` 
mlr.survey1 <- lm(logcost ~ logsize + indcost, data = survey)
summary(___)

# Plot residuals of the fitted model versus `indcost` and superimpose a locally fitted line using the  function [lowess()]
plot(survey$indcost,  ___)
lines(lowess(survey$indcost, ___))

# Regress `logcost` on `logsize` and `indcost` and `indcost` squared
mlr.survey2 <- lm(___ ~ logsize + poly(indcost,2), data = survey)
summary(___)

# Plot residuals of this fitted model and superimpose a locally fitted line using the function [lowess()]
plot(survey$indcost, ___)
lines(lowess(survey$indcost, ___))
```
`@solution`
```{r}
mlr.survey1 <- lm(logcost ~ logsize + indcost, data = survey)
summary(mlr.survey1)

plot(survey$indcost, mlr.survey1$residuals)
lines(lowess(survey$indcost,mlr.survey1$residuals))

mlr.survey2 <- lm(logcost ~ logsize + poly(indcost,2), data = survey)
summary(mlr.survey2)

plot(survey$indcost, mlr.survey2$residuals)
lines(lowess(survey$indcost,mlr.survey2$residuals))
```
`@sct`
```{r}
success_msg("Excellent! In this exercise, you examined residuals from a preliminary model fit and detected a mild quadratic pattern in a variable. This suggested entering the squared term of that variable into the model specification. The refit of this new model suggests that the squared term has important explanatory information. The squared term is a nonlinear alternative that is not available in many automatic variable selection procedures.")
```






---
## Unusual observations

```yaml
type: NormalExercise

xp: 100

key: 4c2ba1533c



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_rhh81ftg&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_58daiyn0" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Compare and contrast three alternative definitions of a standardized residual
- Evaluate three alternative options for dealing with outliers
- Assess the impact of a high leverage observation
- Evaluate options for dealing with high leverage observations
- Describe the notion of influence and Cook's Distance for quantifying influence

`@hint`












---
## Outlier example

```yaml
type: NormalExercise

xp: 100

key: b52fd7ccef



```

In chapter 2, we consider a fictitious data set of 19 "base" points plus three different types of unusual points. In this exercise, we consider the effect of one unusal point, "C", this both an outlier (unusual in the "y" direction) and a high leverage point (usual in the x-space). The data have been pre-loaded in the dataframe `outlrC`.

`@instructions`
- Fit a basic linear regression model of `y` on `x` and store the result in an object.
- Use the function [rstandard()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/influence.measures) to extract the standardized residuals from the fitted regression model object and summarize them. 
- Use the function [hatvalues()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/influence.measures) to extract the leverages from the model fitted and summarize them. 
- Plot the standardized residuals versus the leverages to see the relationship between these two measures that calibrate how unusual an observation is.

`@hint`


`@pre_exercise_code`
```{r}
outlr <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/7a38912e544c31fc6f5fca12b9a2eb645f2bcd32/Outlier.csv", header = TRUE)
outlrC <-outlr[-c(20,21),c("x","y")]
```
`@sample_code`
```{r}
outlrC <- outlr[-c(20,21),c("x","y")]

# Fit a basic linear regression model of `y` on `x` and store the result in an object.
model_outlrC <- lm(y ~ x, data = outlrC)

# Extract the standardized residuals from the fitted regression model object and summarize them.
ri <- rstandard(model_outlrC)
summary(ri)

# Extract the leverages from the model fitted and summarize them. 
hii <- hatvalues(model_outlrC)
summary(hii)

# Plot the standardized residuals versus the leverages
plot(hii,ri)
```
`@solution`
```{r}
plot(outlrC)
model_outlrC <- lm(y ~ x, data = outlrC)
ri <- rstandard(model_outlrC)
summary(ri)
hii <- hatvalues(model_outlrC)
summary(hii)
plot(hii,ri)

```
`@sct`
```{r}
success_msg("Excellent! With only two variables, we could argue graphically that observations were unusual. In this exercise, we showed how statistics could also be used to identify usual observations. Although not really necessary in basic linear regression, the main advantage of the statistics is that they work readily in a multivariate setting.")
```






---
## High leverage and risk manager survey

```yaml
type: NormalExercise

xp: 100

key: c5ee44d248



```

In a prior exercise, we fit a regression model of `logcost` on `logsize`, `indcost` and a squared version of `indcost`. This model is summarized in the object `mlr_survey2`. In this exercise, we examine the robustness of the model to unusual observations. 

`@instructions`
- Use the `R` functions [rstandard()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/influence.measures) and [hatvalues()](https://www.rdocumentation.org/packages/stats/versions/3.5.0/topics/influence.measures) to extract the standardized residuals and leverages from the model fitted. Summarize the distributions graphically.
- You will see that there are two observations where the leverages are high, numbers 10 and 16. On looking at the dataset, these turn out to be observations in a high risk industry. Create a histogram of the variable `indcost` to corroborate this.
- Re-run the regression omitting observations 10 and 16. Summarize this regression and the regression in the object  `mlr_survey2`, noting differences in the coefficients.

`@hint`


`@pre_exercise_code`
```{r}
survey <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/dc1c5bce43ef076aa77169a242118e2e58d01f82/Risk_survey.csv", header=TRUE)
survey$logcost <- log(survey$firmcost)
mlr.survey2 <- lm(logcost ~ logsize + poly(indcost,2), data = survey)
```
`@sample_code`
```{r}
mlr.survey2 <- lm(logcost ~ logsize + poly(indcost,2), data = survey)
# Extract the standardized residuals and leverages from the model fitted. Summarize the distributions graphically.
ri <- ___(mlr.survey2)
hii <- ___(mlr.survey2)
par(mfrow=c(1, 2))
hist(ri, nclass=16, main="", xlab="Standardized Residuals")
hist(hii, nclass=16, main="", xlab="Leverages")

# Create a histogram of the variable `indcost`
par(mfrow=c(1, 1))
hist(___, nclass=16)

# Re-run the regression omitting observations 10 and 16. Summarize this regression and the regression in the object  `mlr_survey2`, noting differences in the coefficients.
mlr.survey3 <- lm(___ ~ logsize + poly(indcost,2), data = survey, subset =-c(10,16))
summary(mlr.survey2)
summary(mlr.survey3)
```
`@solution`
```{r}
#summary(mlr.survey2)
ri <- rstandard(mlr.survey2)
hii <- hatvalues(mlr.survey2)

par(mfrow=c(1, 2))
hist(ri, nclass=16, main="", xlab="Standardized Residuals")
hist(hii, nclass=16, main="", xlab="Leverages")
par(mfrow=c(1, 1))
hist(survey$indcost, nclass=16)
mlr.survey3 <- lm(logcost ~ logsize + poly(indcost,2), data =  survey, subset =-c(10,16))
summary(mlr.survey2)
summary(mlr.survey3)
```
`@sct`
```{r}
success_msg("Excellent! You will have noted that after removing these two influential observations from a high risk industry, the variable associated with the `indcost` squared became less statistically significant. This illustrates a general phenomena; sometimes, the 'signicance' of a variable may actually due to a few unusual observations, not the entire variable.")
```






---
## Collinearity

```yaml
type: NormalExercise

xp: 100

key: 486eada221



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=1_30hrfg77&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=1_khmh83je" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Define collinearity and describe its potential impact on regression inference
- Define a variance inflation factor and describe its effect on a regression coefficients standard error
- Describe rules of thumb for assessing collinearity and options for model reformulation in the presence of severe collinearity
- Compare and contrast effects of leverage and collinearity

`@hint`












---
## Collinearity and term life

```yaml
type: NormalExercise

xp: 100

key: a8e9f1ac3e



```

We have seen that adding an explanatory variable $x^2$ to a model is sometimes helpful even though it is perfectly related to $x$ (such as through the function $f(x)=x^2$). But, for some data sets, higher order polynomials and interactions can be approximately linearly related (depending on the range of the data). 

This exercise returns to our term life data set `Term1` (preloaded) and demonstrates that collinearity can be severe when introducing interaction terms.

`@instructions`
- Fit a MLR model of `logface` on explantory variables `education`, `numhh` and `logincome`
- Use the function [vif()](https://www.rdocumentation.org/packages/car/versions/3.0-0/topics/vif) from the `car` package (preloaded) to calculate variance inflation factors.
- Fit and summarize a MLR model of `logface` on explantory variables `education` , `numhh` and `logincome` with an interaction between `numhh` and `logincome`, then extract variance inflation factors.

`@hint`
If the `car` package is not available to you, then you could calculate vifs using the [lm()] function, treating each variable separately. For example
1/(1-summary(lm(education ~ numhh + logincome, data = Term1))$r.squared)
gives the `education` vif.


`@pre_exercise_code`
```{r}
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
```
`@sample_code`
```{r}
# Fit a MLR model of `logface` on explantory variables `education`, `numhh` and `logincome`
Term_mlr <- lm(logface ~ education + numhh + logincome, data = Term1)

# Calculate the variance inflation factors.
car::vif(Term_mlr)

# Fit and summarize a MLR model of `logface` on explantory variables `education` , `numhh` and `logincome` with an interaction between `numhh` and `logincome`, then extract variance inflation  factors.
Term_mlr1 <- lm(logface ~ education + numhh*logincome , data = Term1)
summary(Term_mlr1)
car::vif(Term_mlr1)
```
`@solution`
```{r}
Term_mlr <- lm(logface ~ education + numhh + logincome, data = Term1)
car::vif(Term_mlr)
Term_mlr1 <- lm(logface ~ education + numhh*logincome , data = Term1)
summary(Term_mlr1)
car::vif(Term_mlr1)
```
`@sct`
```{r}
success_msg("Excellent! This exercise underscores that colinearity among explanatory variables can be induced when introducing higher order terms such as interactions. Note that in the interaction model the variable 'numhh' does not appear to be statistically signficant effect. This is one of the big dangers of collinearity - it can mask important effects.")
```






---
## Selection criteria

```yaml
type: NormalExercise

xp: 100

key: 2536ca544e



```

<iframe id="kaltura_player" src="https://cdnapisec.kaltura.com/p/1660902/sp/166090200/embedIframeJs/uiconf_id/25916071/partner_id/1660902?iframeembed=true&playerId=kaltura_player&entry_id=0_i5dlmsna&flashvars[streamerType]=auto&amp;flashvars[localizationCode]=en&amp;flashvars[leadWithHTML5]=true&amp;flashvars[sideBarContainer.plugin]=true&amp;flashvars[sideBarContainer.position]=left&amp;flashvars[sideBarContainer.clickToClose]=true&amp;flashvars[chapters.plugin]=true&amp;flashvars[chapters.layout]=vertical&amp;flashvars[chapters.thumbnailRotator]=false&amp;flashvars[streamSelector.plugin]=true&amp;flashvars[EmbedPlayer.SpinnerTarget]=videoHolder&amp;flashvars[dualScreen.plugin]=true&amp;&wid=0_kvkokgm2" width="649" height="401" allowfullscreen webkitallowfullscreen mozAllowFullScreen allow="autoplay *; fullscreen *; encrypted-media *" frameborder="0" title="Kaltura Player"></iframe>

`@instructions`
Learning Objectives

In this module, you learn how to:

- Summarize a regression fit using alternative goodness of fit measures
- Validate a model using in-sample and out-of-sample data to mitigate issues of data-snooping

`@hint`












---
## Cross-validation and term life

```yaml
type: NormalExercise

xp: 100

key: 708d227779



```


Here is some sample code to give you a better feel for cross-validation.

The first part of the randomly re-orders ("shuffles") the data. It also identifies explanatory variables `explvars`.

The function starts by pulling out only the needed data into `cvdata`. Then, for each subsample, a model is fit based on all the data except for the subsample, in `train_mlr` with the subsample in `test`. This is repeated for each subsample, then results are summarized.

```
# Randomly re-order data - "shuffle it"
n <- nrow(Term1)
set.seed(12347)
shuffled_Term1 <- Term1[sample(n), ]
explvars <- c("education", "numhh", "logincome")

## Cross - Validation
crossvalfct <- function(explvars){
  cvdata   <- shuffled_Term1[, c("logface", explvars)]
  crossval <- 0
  k <- 5
  for (i in 1:k) {
    indices <- (((i-1) * round((1/k)*nrow(cvdata))) + 1):((i*round((1/k) * nrow(cvdata))))
    # Exclude them from the train set
    train_mlr <- lm(logface ~ ., data = cvdata[-indices,])
    # Include them in the test set
    test  <- data.frame(cvdata[indices, explvars])
    names(test)  <- explvars
    predict_test <- exp(predict(train_mlr, test))
    # Compare predicted to held-out and summarize
    predict_err  <- exp(cvdata[indices, "logface"]) - predict_test
    crossval <- crossval + sum(abs(predict_err))
  }
  crossval/1000
}

crossvalfct(explvars)
```


`@instructions`
- Calculate the cross-validation statistic using only logarithmic income, `logincome`.
- Calculate the cross-validation statistic using `logincome`, `education` and `numhh`.
- Calculate the cross-validation statistic using `logincome`, `education`, `numhh` and `marstat`.

The best model has the lowest cross-validation statistic.

`@hint`
The function [sample()] is for taking random samples. We use it without replacement so it results in a re-ordering of data.

`@pre_exercise_code`
```{r}
#Term <- read.csv("CSVData\\term_life.csv", header = TRUE)
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term1$marstat <- as.factor(Term1$marstat)

crossvalfct <- function(explvars){
  cvdata   <- shuffled_Term1[, c("logface", explvars)]
  crossval <- 0
  k <- 5
  for (i in 1:k) {
    indices <- (((i-1) * round((1/k)*nrow(cvdata))) + 1):((i*round((1/k) * nrow(cvdata))))
    # Exclude them from the train set
    train_mlr <- lm(logface ~ ., data = cvdata[-indices,])
    # Include them in the test set
    test  <- data.frame(cvdata[indices, explvars])
    names(test)  <- explvars
    predict_test <- exp(predict(train_mlr, test))
    # Compare predicted to held-out and summarize
    predict_err  <- exp(cvdata[indices, "logface"]) - predict_test
    crossval <- crossval + sum(abs(predict_err))
  }
  crossval/1000000
}

```
`@sample_code`
```{r}
# Calculate the cross-validation statistic using only logarithmic income, `logincome`.
explvars <- c("logincome")
crossvalfct(explvars)

# Calculate the cross-validation statistic using `logincome`, `education` and `numhh`.
explvars <- c("education", "numhh", "logincome")
crossvalfct(___)

# Calculate the cross-validation statistic using `logincome`, `education`, `numhh` and `marstat`.
explvars <- c(___)
crossvalfct(explvars)
```
`@solution`
```{r}
# Randomly re-order data - "shuffle it"
n <- nrow(Term1)
set.seed(12347)
shuffled_Term1 <- Term1[sample(n), ]
## Cross - Validation
explvars <- c("logincome")
crossvalfct(explvars)
explvars <- c("education", "numhh", "logincome")
crossvalfct(explvars)
explvars <- c("education", "numhh", "logincome", "marstat")
crossvalfct(explvars)
```





