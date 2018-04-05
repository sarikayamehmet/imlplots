
imlplots: interpretable machine learning plots
==============================================

`imlplots` is an R package that provide an interactive Shiny dashboard for three kinds of Interpretable Machine Learning (IML) plots

-   Partial Dependence Plots (PDP)
-   Individual Conditional Expectation (ICE) plots
-   Accumulated Local Effect (ALE) plots

Installation
============

The package can be installed directly from github with devtools:

``` r
# install.packages("devtools")
devtools::install_github('riebetob/imlplots')
library(imlplots)
```

Quickstart
==========

You can fit classification and regression problems from the `mlr` package and analyse possible interaction effects in the Shiny dasbhoard.

For quickstart we take the popular Boston Housing data, where we want to predict the median housing price in Boston.

``` r
library(MASS)
data(Boston)
```

For using `imlplots` Shiny dashboard, three input arguments need to be specified

-   `data` - the input data
-   `task`- the learning task
-   `models` - one or several trained models

We create a regression task with `medv` as target variable. The task structure is determined by `mlr` package.

``` r
library(mlr)
boston.task = makeRegrTask(data = Boston, target = "medv")
```

The `imlplots` dashboard allows the comparison of multiple learning algorithms, therefore we fit two different models - first a random forest and second a SVM.

``` r
rf.mod = train("regr.randomForest", boston.task)
svm.mod = train("regr.ksvm", boston.task)
```

The input for the Shiny app is a list of learners.

``` r
mod.list = list(rf.mod, svm.mod)
```

Now the Shiny app can be used.

``` r
imlplots(data = Boston, task = boston.task, models = mod.list)
```

References
==========

-   [PDP and ICE plots](https://arxiv.org/pdf/1309.6392.pdf)
-   [mmpf R package](https://github.com/zmjones/mmpf)
-   [ALE plots](https://arxiv.org/abs/1612.08468)
-   [ALE R package](https://cran.r-project.org/web/packages/ALEPlot/index.html)
