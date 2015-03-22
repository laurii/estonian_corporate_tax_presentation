---
title       : Estonian Tax defaults 
subtitle    : Corporate Tax defaults data as of 19.02.2015
author      : Lauri Ilison
job         : Data Analyst
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

## About the Estonia Tax system

The Estonian tax system consists of national taxes and local taxes collected by local governments in their jurisdiction. National taxes include income tax, social tax, land tax, gambling tax, value-added tax, duty and excise taxes and heavy goods vehicle tax. Local governments have the authority to impose local taxes, but effectively only a few have introduced local taxes, in particular: boat tax, advertisement tax, tax for closing of streets, motor vehicle tax, tax on keeping domestic animals, amusement tax, and parking fees.

Estonia does not impose any gift, inheritance or estate taxes. Various transactions may be subject to payment of state fees (stamp duties).

Estonia is a small country with 1.3 MIO citizens with the GDP of $36.947 billion.
Estonia has shown its abilty to collect nearly all taxes.
At the current stage - the tax GAP (non paid taxes) is about 300 MIO EUR per year
Currently there is ca 110 MIO EUR defaults of taxes by Corporates

--- .class #id 

## Corporate Taxes in Estonia

Estonian resident companies and permanent establishments of the foreign entities (including branches) are subject to income tax only in respect of all distributed profits (both actual and deemed), including:

1. corporate profits distributed in the tax period;
2. gifts, donations and representation expenses;
3. expenses and payments not related to business.

Fringe benefits are taxable at the level of employer. The employer pays income tax and social tax on fringe benefits.

All distributions are subject to income tax at the rate of 20% of the amount of taxable payment. The transfer of assets of the permanent establishment to its head office or to other companies is also treated like a distribution. As of 1 January 2009, dividends paid to non-residents are no longer subject to withholding tax at the general rate of 20%, irrespective of participation in the share capital of the distributing Estonian company. However, various withholding taxes may still apply to other payments to non-residents if they do not have a permanent establishment in Estonia or unless the tax treaties otherwise provide.

--- .class #id

## Top Tax Default Companies

Top Companies with Defaulted Taxes

```r
library(data.table)
library(ggplot2)
DT <- as.data.table(readRDS('Estoninan_companies_tax_defaults_as_of_17.02.2015.rds'))
setnames(DT,c("RegistrationID", "CompanyName","TaxSumInDefault","InclTaxSumInDispute","DefaultStartDate"))
head(DT[order(-rank(TaxSumInDefault))],n = 15)
```

```
##     RegistrationID                 CompanyName TaxSumInDefault
##  1:       11330410                  TABEYO, OÜ       4053831.0
##  2:       11413107         FUND INVESTMENTS OÜ       1650521.0
##  3:       10259970          OZON MMG GRUPP, OÜ       1409109.0
##  4:       10046635                 BITEST, TÜH       1380435.1
##  5:       12584408           BALTIC TÖÖJÕUD OÜ       1148723.5
##  6:       12603614          SIMETRA TÖÖJÕUD OÜ       1051713.8
##  7:       11222270           ADRIAN ARENDUS OÜ        990663.0
##  8:       11901539 VIVA ELEKTROONIKA PLUSS, OÜ        952075.0
##  9:       10853672            ROSNEFT EESTI OÜ        835363.5
## 10:       10934761            JALAKA INVEST OÜ        833897.7
## 11:       10261486 INIMÕIGUSTE KAITSE BÜROO OÜ        800261.8
## 12:       12102208           COMPUTER PARTS OÜ        738500.0
## 13:       12237842                LOORVALT, OÜ        601880.6
## 14:       11402380                 SIMCITY, OÜ        565108.8
## 15:       11626263             RKO PLATVORM OÜ        543835.7
##     InclTaxSumInDispute DefaultStartDate
##  1:                 0.0       2012-02-20
##  2:                 0.0       2013-05-10
##  3:                 0.0       2012-01-10
##  4:                 0.0       2013-06-17
##  5:                 0.0       2014-02-10
##  6:                 0.0       2014-12-22
##  7:                 0.0       2012-09-20
##  8:            141211.9       2011-09-20
##  9:                 0.0       2007-05-21
## 10:                 0.0       2013-05-20
## 11:                 0.0       2007-04-20
## 12:                 0.0       2011-07-20
## 13:                 0.0       2012-04-10
## 14:                 0.0       2013-01-10
## 15:                 0.0       2009-12-21
```


--- .class #id 
## Tax defaults by first appearacne date

```r
qplot(x = DefaultStartDate,y = TaxSumInDefault,data=DT,xlab = "Default Start Date", ylab = "Tax Default in EUR", main = "Tax Defaults by frist apparance date")
```

![plot of chunk unnamed-chunk-2](assets/fig/unnamed-chunk-2-1.png) 

---
## Tax defaults historgram for large defaults

```r
hist(DT[TaxSumInDefault > 100000,TaxSumInDefault],breaks=100, xlab = "Tax default in EUR", ylab = "Number of Companies", main = "Companies Tax default > 100000 EUR")
```

![plot of chunk unnamed-chunk-3](assets/fig/unnamed-chunk-3-1.png) 

Companies with defaults bigger than 100'000 EUR



