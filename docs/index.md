# pssbounds
Module to display the necessary critical values to conduct the Pesaran, Shin and Smith (2001) bounds test for cointegration. This is available for both Stata and R.

## Download

### Stata
The most recent Stata version of `pssbounds`  can be downloaded by clicking [here](https://github.com/andyphilips/pssbounds/archive/master.zip). This program is part of a suite that also includes `dynpss`, a program to dynamically simulate autoregressive distributed lag models, available [HERE](http://andyphilips.github.io/dynpss/). See [Jordan and Philips](https://github.com/andyphilips/pssbounds/raw/master/files/pss_Stata_2017.pdf) (2017) for an in-depth discussion of this program.

### R
In R, the `pssbounds` function is part of the `pss` package, available [HERE](https://github.com/andyphilips/pss). To download pss, you will need to obtain the devtools package and make a call from R to GitHub:

```r
install.packages("devtools")
library(devtools)
install_github("andyphilips/pss")
library(pss)
```
You should now be ready to use pss.

## Table of Contents
  * [Description](#description)
  * [Syntax](#syntax)
     * [Stata](#syntaxstata)
     * [R](#syntaxr)
  * [Reference](#reference)
  * [Authors](#authors)
  * [Citations](#citations)
  * [Examples](#examples)
     * [Stata](#examplestata)
     * [R](#exampler)
  * [Version](#version)

## Description<a id="description"></a>
`pssbounds` is a module that displays the necessary critical values to conduct the Pesaran, Shin and Smith (2001, henceforth PSS) bounds test for cointegration. It is available for both Stata and R.

As discussed in Philips (2017), the upper and lower bounds of the PSS cointegration test are non-standard, and depend on the number of observations, the number of regressors (k) appearing in levels, and the restrictions (if any) placed on the intercept and trend (called a case). Asymptotic critical values are provided by PSS (2001), while small-sample critical values are from Narayan (2005). The following five cases are possible: I (no intercept, no trend), II (restricted intercept, no trend), III (unrestricted intercept, no trend), IV (unrestricted intercept, restricted trend), V (unrestricted intercept, unrestricted trend). See PSS (2001) for more details; Case III is the most common.

`pssbounds` assumes that you have already run the ARDL-bounds model, ensured white-noise residuals, and have obtained the statistic from an F-test on the restriction that all variables appearing in levels are jointly equal to zero (see Philips 2017 for examples of this procedure). The bounds test for cointegration has three possible outcomes. If the value of the F-statistic lies outside the I(0) critical value (or lower "bound"), the test fails to reject the null hypothesis and we may conclude that all regressors appearing in levels are in fact stationary. If the value of the F-statistic lies outside the I(1) critical value (upper "bound"), the test rejects the null hypothesis and we may conclude that cointegration exists. If the value of the F-statistic lies between the I(0) and I(1) critical values, the test is inconclusive.

`pssbounds` also provides the critical values of an optional t-test for cointegration. It can be used to test the null hypothesis that the coefficient on the lagged dependent variable is equal to zero, although note that the upper and lower I(0)-I(1) bounds are exactly the opposite as for the F-test. No small-sample critical values are currently available for this test, so these are asymptotic approximations, and no values are available for cases II or IV.


## Syntax<a id="syntax"></a>
### Stata<a id="syntaxstata"></a>

```do
pssbounds , observations(#) fstat(#) k(#) [tstat(#) case(#)]
```

#### Required options
* `observations(#)` is the number of observations (i.e. length of the series) from the ARDL-bounds model. Since the critical values of the bounds test depend on the size of the sample, this option is required.
* `fstat(#)` is the value of the F-statistic from the test that all variables appearing in levels are jointly equal to zero. This can be obtained by using Stata's `test` command.
* `k(#)` is the number of regressors appearing in levels in the ARDL-bounds model. Since the critical values of the bounds test depend on the number of regressors, this option is required.

#### Additional options
* `tstat(#)` is the value of the one-sided t-test that the coefficient on the lagged dependent variable is equal to zero. Only asymptotic critical values are currently available, and only for cases I, III, and V.
* `case(#)` identifies the type of case of the restrictions on the intercept and/or trend term. Case type can be given in Roman numerals (I,II,III,IV,V) or numerically (1,2,3,4,5). Since the critical values of the bounds test depend on the assumptions placed on the intercept and trend, this option is required.

### R<a id="syntaxr"></a>

```r
pssbounds(obs, fstat, tstat=NULL, case, k)
```

#### Required options
* `obs` is the number of observations (i.e. length of the series) from the ARDL-bounds model. Since the critical values of the bounds test depend on the size of the sample, this option is required.
* `fstat`is the value of the F-statistic from the test that all variables appearing in levels are jointly equal to zero.
* `case` identifies the type of case of the restrictions on the intercept and/or trend term. Case type can be given in Roman numerals ("I","II","III","IV","V") or numerically (1,2,3,4,5). Since the critical values of the bounds test depend on the assumptions placed on the intercept and trend, this option is required.
* `k`is the number of regressors appearing in levels in the ARDL-bounds model. Since the critical values of the bounds test depend on the number of regressors, this option is required.

### Additional options
* `tstat` is the value of the one-sided t-test that the coefficient on the lagged dependent variable is equal to zero. Only asymptotic critical values are currently available, and only for cases I, III, and V.

## Reference<a id="reference"></a>
If you use `pssbounds` in Stata, please cite:

Jordan, Soren and Andrew Q. Philips. 2017 "[Cointegration testing and dynamic simulations of autoregressive distributed lag models](https://github.com/andyphilips/pssbounds/raw/master/files/pss_Stata_2017.pdf)". Working Paper.

and

Philips, Andrew Q. 2017. "[Have your cake and eat it too? Cointegration and dynamic inference from autoregressive distributed lag models](http://dx.doi.org/10.1111/ajps.12318)." American Journal of Political Science.

If you use `pssbounds` in R, please cite:

Jordan, Soren and Andrew Q. Philips. 2016. "[pss: R package to perform the bounds test for cointegration and perform dynamic simulations](https://github.com/andyphilips/pss)."

and

Philips, Andrew Q. 2017. "[Have your cake and eat it too? Cointegration and dynamic inference from autoregressive distributed lag models](http://dx.doi.org/10.1111/ajps.12318)." American Journal of Political Science.

## Authors<a id="authors"></a>
[Andrew Q. Philips](http://www.andyphilips.com), Department of Political Science, University of Colorado at Boulder. andrew.philips [AT] colorado.edu. @andyphilips

and

[Soren Jordan](http://sorenjordan.com), Department of Political Science, Auburn University. sorenjordanpols [AT] gmail.com.

## Citations<a id="citations"></a>
Narayan, Paresh Kumar. 2005. "The Saving and Investment Nexus for China: Evidence from Cointegration Tests." Applied Economics 37(17):1979-1990.

Pesaran, M Hashem, Yongcheol Shin and Richard J Smith. 2001. "Bounds testing approaches to the analysis of level relationships." Journal of Applied Econometrics 16(3):289-326.


## Examples<a id="examples"></a>

### Stata<a id="examplestata"></a>

See the [working paper](https://github.com/andyphilips/pssbounds/raw/master/files/pss_Stata_2017.pdf) for up-to-date examples of `pssbounds` in action.

### R<a id="exampler"></a>

```r
library(MASS)
library(car)
data("airquality")
d.wind <- c(NA,diff(airquality$Wind))
d.temp <- c(NA,diff(airquality$Temp))
l.wind <- lag(airquality$Wind, k = 1)
l.temp <- lag(airquality$Temp, k = 1)
cbind(d.wind, d.temp, l.wind, l.temp)
```
Run an error-correction model with the following regressors: the first difference of temp, and the lagged-levels of temp and wind (white-noise residuals assumed):

```r
res <- lm(d.temp ~ l.temp + l.wind + d.wind)
summary(res) # t-stat on l.temp = 4.438
```
Perform F-test:

```r
linearHypothesis(res, c("l.temp = 0", "l.wind = 0")) # 9.8789
```
Grab critical values from bounds test:

```r
bounds <- pssbounds(obs = 153, case = 3, k = 1, fstat = 9.879, tstat = 4.438)
```
F-statistic bounds test concludes I(1) and cointegrating, but the t-statistic test concludes all I(0) regressors.

Run the same model excluding the constant:

```r
res2 <- lm(d.temp ~ l.temp + l.wind + d.wind - 1)
summary(res2) # t-stat on l.temp =  1.445
linearHypothesis(res2, c("l.temp=0","l.wind = 0")) # 1.045
bounds2 <- pssbounds(case = 1, tstat = 1.445, fstat = 1.045, obs = 153, k = 1)
```
Now the bounds F-statistic test concludes I(0) regressors. 

## Version <a id="version"></a>
Stata version: 1.0.5; R version: 0.1.3.9000.
