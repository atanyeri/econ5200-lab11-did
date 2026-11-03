# Difference-in-Differences: Parallel Trends, Staggered Adoption and the Forbidden Comparison

## Objective
I tested when difference-in-differences gives the right answer and when it does not, using the original Card and Krueger data and simulated panels where I knew the true effect.

## Methodology
- Reproduced Card and Krueger's (1994) New Jersey and Pennsylvania fast-food comparison from David Card's original data files, using full-time-equivalent employment as the outcome.
- Built a panel where the true effect was zero but the treated and control groups were on different trends. I ran the DiD regression, then plotted group means and ran a pre-trend test.
- Built a staggered-adoption panel with an early and a late cohort, all true effects positive and a true mean of 6.71. I fit two-way fixed effects and rebuilt the coefficient by hand as a weighted average of two two-by-two comparisons.
- Wrote a clean estimator that only uses not-yet-treated units as controls, and packaged it as a reusable module.
- Simulated a state-level policy with shocks that persist from period to period, and compared iid standard errors with standard errors clustered by state.
- Had an AI write a Goodman-Bacon decomposition and checked it against my own numbers on two panels, one of them with missing outcomes. I revised my prompt once after the first version failed on the panel with missing outcomes.
- Plotted an event study with pre-period estimates, and sketched a simplified bound on how much the result depends on parallel trends.

## Key Findings
- I reproduced Card and Krueger's result at 2.75 full-time-equivalent employees, against their published +2.76.
- On the panel with different trends, the DiD estimate was large and significant even though the true effect was zero. The pre-trend test caught it, but a test that passes would not have shown that parallel trends held.
- Two-way fixed effects returned -0.99 on the staggered panel, where the true mean effect was 6.71. Two-thirds (0.667) of the weight sat on the comparison that uses already-treated units as controls, and that comparison came out negative.
- iid standard errors were 8.6 times too small on the panel with persistent state shocks. Clustering by state fixed most of this, though the test still rejected a true null more often than 5% of the time.
- My first prompt to the AI left out how to handle missing outcomes, and the function stopped with an error. After I revised the prompt, its weighted sum on the panel with missing outcomes was 2.6735, which matched the two-way fixed effects coefficient.
