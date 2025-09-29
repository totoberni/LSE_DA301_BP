# Strategic Plan: Customer Segmentation with Advanced Tree-Based Models

## 1. Executive Summary

This document outlines a strategic plan to move beyond simple prediction and create actionable customer segments for Turtle Games' marketing department. Building directly on the **`CustomerValueScore`** engineered in the Week 1 analysis, this plan will leverage a suite of advanced tree-based models. Our objective is to transition from understanding *what* drives value (regression) to understanding *who* the high-value customers are and *how* to identify them with clear, data-driven rules (segmentation).

The approach is structured in three phases:
1.  **Interpretability:** Build an optimally pruned decision tree to generate a transparent, rule-based model of customer value.
2.  **Accuracy:** Implement a Random Forest to validate our key drivers and improve predictive performance.
3.  **Explainability:** Deploy a state-of-the-art XGBoost model and pair it with SHAP (SHapley Additive exPlanations) to achieve both maximum accuracy and full model transparency.

This strategy is designed to deliver a "High Distinction" level of analysis by providing deep, explainable, and commercially valuable customer personas.

---

## 2. Advanced Model Implementation Plan

Our goal is to build a hierarchy of models that predict the `CustomerValueScore`, balancing interpretability with predictive power. We will use the fully-featured dataset (`rdf8`) from the previous section, which includes the engineered sentiment scores and the `CustomerValueScore` target variable.

### 2.1. Phase 1: The Interpretable Baseline (Optimal Decision Tree)

The primary goal of this phase is to create a single, clear, and statistically robust decision tree that provides an initial set of segmentation rules.

**a. Advanced Pruning (Cost-Complexity Pruning):**
   - Instead of manually guessing `max_depth`, we will implement **Cost-Complexity Pruning** (`ccp_alpha`).
   - **Process:** First, train a full, unpruned decision tree. Then, use cross-validation to find the optimal `ccp_alpha` value, which represents the best trade-off between model complexity and predictive accuracy.
   - **Benefit:** This is a data-driven approach that produces an optimally sized tree, maximizing interpretability without sacrificing significant predictive power.

**b. Tree Visualization and Rule Extraction:**
   - Visualize the final pruned tree. This visualization will serve as a direct "map" of the rules the model has learned to segment high-value and low-value customers.
   - We will manually extract 3-4 of the most important paths in the tree to form our initial customer personas (e.g., "High Income, Young Spender").

### 2.2. Phase 2: The Robust Predictor (Random Forest)

This phase aims to improve accuracy and validate our findings from Phase 1 using an ensemble method.

**a. Model Implementation and Tuning:**
   - Implement a `RandomForestRegressor`.
   - Use `GridSearchCV` or `RandomizedSearchCV` to tune key hyperparameters like `n_estimators` (number of trees), `max_features`, and `max_depth`.

**b. Feature Importance Validation:**
   - The primary output of this phase will be the Random Forest's feature importance ranking.
   - **Strategic Goal:** We will compare this ranking directly against the permutation importance results from our Week 1 SVR model. If `income` and `age` remain the top predictors, it provides powerful, cross-model validation of our findings. This demonstrates analytical rigor.

### 2.3. Phase 3: The Explainable Powerhouse (XGBoost + SHAP)

This phase delivers the pinnacle of analysis: a state-of-the-art predictive model combined with a cutting-edge interpretation framework. This provides the accuracy of a "black box" model with the transparency of a simple one.

**a. XGBoost Implementation:**
   - Implement an `XGBoost Regressor`, a highly efficient and powerful gradient boosting algorithm.
   - Perform hyperparameter tuning to maximize its predictive accuracy on the `CustomerValueScore`. This model will represent our most accurate predictive tool.

**b. Unlocking the "Black Box" with SHAP:**
   - **What is SHAP?** SHAP (SHapley Additive exPlanations) is a game-theoretic approach to explain the output of any machine learning model. It quantifies the contribution of each feature to an individual prediction.
   - **Implementation:**
     1.  Initialize a SHAP `TreeExplainer` with our trained XGBoost model.
     2.  Calculate SHAP values for all customers in our test set.
   - **Outputs & Business Value:**
     - **Global Importance (Summary Plot):** Generate a SHAP summary plot. This is more informative than standard feature importance plots as it shows not only the magnitude but also the *direction* of each feature's effect (e.g., it will visually confirm that high `income` positively impacts the value score, while low `income` negatively impacts it).
     - **Individual Prediction Explanation (Force Plots):** Select examples of key customer profiles (e.g., a high-value customer, a low-value customer) and generate SHAP force plots for them. This plot will provide a crystal-clear, quantitative explanation for their predicted score, such as: *"This customer's high predicted value is driven by their `income` (+0.25), and their `age` (+0.10), despite their neutral `review_sentiment` (-0.05)."*

---

## 3. Customer Segmentation and Marketing Strategy

The final output of this analysis will be a set of clearly defined customer personas with tailored marketing recommendations.

**a. Define Core Customer Personas:**
   - Use the rules extracted from the pruned decision tree (Phase 1) to create 3-4 named personas.
   - **Example Personas:**
     - **"The High-Value Professional":** (e.g., `income` > £75k, `age` < 35). High value, likely to be early adopters.
     - **"The Cautious Earner":** (e.g., `income` > £75k, `spendingScore` < 40). High potential but needs encouragement.
     - **"The Engaged Enthusiast":** (e.g., `income` < £40k, `spendingScore` > 80). Lower income but highly active; potential brand advocates.

**b. Enrich Personas with SHAP Insights:**
   - Use the SHAP findings (Phase 3) to add depth to these personas. For "The Cautious Earner," we can use SHAP to confirm that their `income` is a strong positive driver while their spending habits are a negative driver, validating the need for targeted activation campaigns.

**c. Propose Actionable Marketing Strategies:**
   - For each persona, propose a specific, data-driven marketing action.
     - **"High-Value Professional":** Target with loyalty program exclusives and early access to new products.
     - **"Cautious Earner":** Target with personalized offers or "bundle and save" promotions to increase their spending confidence and unlock their potential value.
     - **"Engaged Enthusiast":** Target with community-building initiatives and referral programs to leverage their brand advocacy.