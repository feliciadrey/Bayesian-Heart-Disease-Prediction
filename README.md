# Bayesian Cardiovascular Disease Prediction

This project explores the application of **Bayesian logistic regression** to predict heart disease using the [Heart Disease Prediction Dataset](https://www.kaggle.com/datasets/krishujeniya/heart-diseae). Two Bayesian models were developed and compared:

1. **Model 1: Logistic Regression with Uninformative Priors**

   * Priors: flat/weakly informative (𝛽 \~ N(0, 0.01))
   * Baseline model for comparison.

2. **Model 2: Logistic Regression with Informative Priors**

   * Priors derived from **published clinical studies** (odds ratios and CIs transformed into prior distributions).
   * Incorporates domain knowledge into the Bayesian framework.

The models were estimated using **JAGS** via MCMC sampling, with convergence diagnostics, posterior summaries, and model comparison conducted in R.

---

## Dataset

The dataset contains patient medical attributes used to assess the likelihood of cardiovascular disease.

**Key features include:**

* Age, Sex
* Chest pain type (cp)
* Resting blood pressure (trestbps)
* Cholesterol (chol)
* Fasting blood sugar (fbs)
* Resting ECG (restecg)
* Maximum heart rate (thalach)
* Exercise-induced angina (exang)
* ST depression (oldpeak)
* Slope of ST segment, number of major vessels (ca), thalassemia (thal)
* **Target**: presence of heart disease

---

##  Methodology

* **MCMC Settings:**

  * Burn-in: 1000 iterations
  * Post-burn-in samples: 5000
  * Chains: 2
  * Thinning: 5

* **Convergence Diagnostics:**

  * Trace plots & autocorrelation plots
  * Effective Sample Size (ESS)
  * Gelman-Rubin statistic (PSRF)
  * Geweke diagnostic

* **Model Comparison Metrics:**

  * Bayes Factor
  * WAIC (Watanabe–Akaike Information Criterion)
  * LOO (Leave-One-Out Cross Validation)

* **Posterior Predictive Checks** to assess model fit.

---

## Results

* **Convergence:**
  Both models showed good convergence (ESS high, PSRF < 1.1, |z| < 2 for Geweke).

* **Model Comparison:**

  * **Model 2** (informative priors) had a **lower WAIC (≈ 365)** compared to **Model 1 (≈ 415)**.
  * Bayes Factor slightly favored Model 2.
  * LOO-CV also indicated Model 2 had better predictive accuracy.

* **Significant Predictors (Model 2):**

  * Age
  * Sex
  * Chest Pain Type (cp)
  * Resting Blood Pressure (trestbps)
  * Cholesterol (chol)
  * Resting ECG (restecg)
  * Exercise-induced Angina (exang)
  * ST Depression (oldpeak)
  * Number of Major Vessels (ca)
  * Thalassemia (thal)

* **Posterior Predictive Check:**
  Despite improved fit, Model 2 still showed some **misfit** (low p-value ≈ 0.008), indicating predictions underestimated the observed proportion of positive cases.

---

## Conclusion

* Incorporating informative priors (**Model 2**) improved predictive performance compared to uninformative priors (**Model 1**).
* Significant clinical predictors of heart disease were identified, consistent with existing literature.
* However, posterior predictive checks suggest the model could be refined further by:

  * Improving prior specification
  * Including additional covariates (e.g., lifestyle factors, family history)
  * Validating with external datasets

---

## Acknowledgment

This project was completed as part of a group collaboration. Credit is due to my team for their contributions in data preparation, modeling, and discussion.
