# Retention Strategies Based on Churn Risk

These are hypotheses to validate with controlled experiments, not guaranteed causal effects. Use model risk scores to prioritize a human-reviewed outreach queue; do not automatically deny services or apply punitive treatment.

## 1. Month-to-month customers with short tenure
**Signal to inspect:** month-to-month contract and low tenure are commonly associated with higher churn in the Telco sample. Confirm this in the current SHAP plots and segment tables before operational use.
**Action:** offer an onboarding check-in, explain plan features, and provide an opt-in annual-plan comparison where it genuinely benefits the customer.
**Measure:** 30/60/90-day retention, opt-in rate, complaints and margin. A/B test against business-as-usual.

## 2. Customers with high monthly charges or perceived value gaps
**Signal to inspect:** elevated MonthlyCharges or a mismatch between plan and service use may appear in global/local explanations.
**Action:** conduct a plan-fit review, clearly explain charges, and offer a lower-cost or better-fitting plan when appropriate. Avoid blanket discounts to customers who do not need them.
**Measure:** churn rate, revenue retained, plan changes, customer satisfaction and discount cost.

## 3. Customers without support/security add-ons who show risk
**Signal to inspect:** lack of OnlineSecurity or TechSupport may be associated with churn in the model; verify direction and stability rather than assuming causality.
**Action:** offer a brief setup/support session or a transparent trial/feature walkthrough. Ensure the offer is relevant and voluntary.
**Measure:** support adoption, repeat contacts, churn and cost per retained customer.

## Operating safeguards
- Explain that SHAP values describe model contribution, not why a customer will definitely leave.
- Compare outcomes across customer segments and investigate material performance disparities.
- Respect consent, contact preferences, applicable privacy rules and retention policies.
- Do not expose raw customer identifiers in reports or presentations.
- Review intervention outcomes; stop strategies that increase complaints or create unfair treatment.
