# Synthetic Control and Heterogeneous Treatment Effects in Healthcare Policy

**Sentinel Analytics** | Causal Inference Consulting 

---

This project applies two causal inference frameworks to real healthcare policy questions, using R and Quarto. The goal throughout is not just statistical accuracy but decision-relevant insight: what actually happened, who was affected, and what should a healthcare organization do about it?

---

## Case 1: Did California's Medicaid Expansion Reduce Mortality?

California expanded Medicaid in 2014 under the ACA. The California Health Board asked whether this expansion causally reduced all-cause mortality rates across the state.

Because only one state received the treatment, standard regression approaches do not apply. We used **Synthetic Control** to build a weighted combination of non-expanding states that closely matched California's pre-2014 mortality trajectory, then used this synthetic counterpart as the counterfactual.

Confounders accounted for include median household income, the uninsured rate, hospital beds per 1,000 residents, and the share of population aged 65 and older.

---

## Case 2: Does Telemedicine Work, and for Whom?

The Regional Health Alliance (RHA) serves over 500,000 patients across urban, suburban, and rural communities in the Southeastern US. After investing $12 million in telemedicine infrastructure during COVID-19, leadership needed to know whether the program was worth sustaining and, more importantly, whether its benefits were consistent across their diverse patient population.

Their average outcomes looked nearly flat. But averages can hide a lot.

We used **Heterogeneous Treatment Effects** methods to uncover how telemedicine's impact varied by patient age, finding a clear and statistically significant age gradient.

### Methods

- **S-Learner, T-Learner, X-Learner** (Meta-Learners): machine learning approaches that estimate individualized treatment effects using a single model, separate models per treatment group, and a propensity-weighted combination respectively
- **Causal Random Forest (CRF)**: doubly-robust, honest estimation of conditional average treatment effects (CATEs), with Best Linear Projection and RATE analysis for validation

### Key Findings

Telemedicine has a positive average treatment effect of roughly 0.98 HRQoL points, which is statistically significant but practically small. The real story is underneath that average:

- Patients **under 45** experience negative effects from telemedicine (roughly -1 to -4 HRQoL points). Digital friction and lower health complexity likely outweigh the convenience benefit.
- Patients **50 and older** see consistent positive effects (+2 to +3.5 HRQoL points), driven by chronic disease management needs, mobility constraints, and schedule flexibility.
- The **crossover point is around age 45 to 50**, confirmed across all four estimation methods and formally validated by the CRF's Best Linear Projection (coefficient: +0.124 per year of age, p < 0.001).
- The **RATE curve** confirms the CRF rankings are actionable: targeting high-CATE patients yields meaningfully better outcomes than treating everyone uniformly.

### Business Recommendation

RHA spends $6.2M annually on telemedicine. Based on CATEs, redirecting outreach toward patients 50 and older (approximately 55% of their patient base) while supplementing younger patients with hybrid support would maximize aggregate health gains within the same budget. The heterogeneity evidence also gives RHA a compelling case for age-stratified Medicaid reimbursement policies.

---

## Tech Stack

- **Language:** R
- **Report format:** Quarto (.qmd), rendered to self-contained HTML
- **Key packages:** `grf`, `caret`, `ggplot2`, `dplyr`, `knitr`

---

## Authors

Arpita Ram Samant, Victor Ostolaza, Vedaant Rath, Sam Sheng, Muhammad Sawaiz Fatar
