---
title: "ECLS-K-2011"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Multilevel testing assumptions
```{r}
install.packages("DHARMa")
library(DHARMa)

library(lme4)
data("InstEval")
head(InstEval)

fmCross = lmer(y~ 1 + (1|s), InstEval, REML = FALSE)

simulationOutput <- simulateResiduals(fittedModel = fmCross, n = 250)

test = simulationOutput$scaledResiduals
qqnorm(test)

plotSimulatedResiduals(simulationOutput = simulationOutput)

testUniformity(simulationOutput = simulationOutput)

```

