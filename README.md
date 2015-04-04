# PETPEESE
Functions for R to make PET-PEESE modeling and output easier.

# PET-PEESE meta-regression
PET-PEESE meta-regression is a means to detect and adjust for small-study effects. 
Most typically these small-study effects are expected to reflect publication bias, but be warned that they can also reflect
genuine differences in study effects and study designs (e.g. correlational research having larger samples and larger effects
than experimental research).

I don't know how to use the global/local environments well so for now everything assumes you're running fixed-effects models
on Fisher's Z using column names such that Comprehensive Meta-Analysis v3 spits out.

# PET()
PET() returns an rma object, treating the standard error as a moderator. 
This inspects for a linear relationship between precision and effect size akin to Egger's regression test.
It will underestimate the effect when there is a true effect.
You can inspect influence diagnostics with influence(PET()) or plot them with plot(influence(PET())).

# PEESE()
PEESE() returns an rma object, treating the variance as a moderator.
This inspects for a curvilinear relationship between precision and effect size such that imprecise studies have bias,
but precise studies have more signal and less bias.
It will overestimate the effect when there is no true effect.
You can inspect influence diagnostics with influence(PET()) or plot them with plot(influence(PET())).

# funnelPETPEESE()
funnelPETPEESE() creates a funnel plot of the data, overlays the PET regression line, and, if appropriate, overlays the
PEESE regression line.
PEESE is only returned if the estimate from PET is significantly different from zero. This can be overridden by specifying
the argument alwaysPEESE = T.
Text output compares the PET estimate and p-values, PEESE estimate, and naive meta-analytic estimate.
Note that the package assumes Fisher's Z in the raw data and converts to Pearson r for the text output.

# Why rma() and not lm()?
I don't fully understand it myself but the author of 'metafor' has written about it extensively here: 
http://www.metafor-project.org/doku.php/tips:rma_vs_lm_and_lme
It seems that lm() overestimates the degree of error variance and will not properly weight the observations.
