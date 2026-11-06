# Data Analyst Interview Preparation

## Technical questions

### 1. What does a `LEFT JOIN` do?

A `LEFT JOIN` returns every row from the left table and matching rows from the right table. If there is no match, the right-table columns are `NULL`. It is useful when I need to retain the full population in my primary table—for example, all customers, including those with no transactions. I check join-key uniqueness and row counts because duplicate keys on the right can multiply rows.

### 2. How do you handle missing data?

First I quantify missingness by column and segment, check whether it is caused by collection or processing, and assess whether it may be systematic. I then choose a treatment based on meaning and analysis: correct the source, retain and flag missing values, exclude only when justified, or impute with a documented method. I compare results with and without imputation and report the limitations; I do not automatically replace missing values with zero.

### 3. When would you use the mean versus the median?

The mean uses every value and is useful for fairly symmetric data when the arithmetic average is meaningful. It is sensitive to extreme values. The median is the 50th percentile and is more robust for skewed distributions, such as transaction amounts with a few very large purchases. I inspect the distribution and often report both when skew matters.

### 4. What does a p-value mean?

A p-value is the probability, assuming the null hypothesis and the test assumptions are true, of observing a result at least as extreme as the one measured. It is not the probability that the null hypothesis is true, nor does it measure business importance. In my synthetic PesaPap onboarding analysis, the chi-square p-value of 0.0052 is evidence against equal conversion rates; I also report the 3.34 percentage-point observed difference and its 95% confidence interval.

### 5. How would you investigate a sudden drop in sales?

I would first confirm the drop is real: validate source freshness, row counts, date/time handling, refunds, and metric definitions. Then I would compare the same time period with appropriate prior periods and break results down by product, branch, channel, customer segment, and funnel stage. I would look for a concentrated driver, quantify its contribution, and check operational or external changes with stakeholders. I would present the evidence and uncertainty, recommend a targeted action, and monitor the metric and guardrails after the change.

## Behavioural questions (STAR)

### 1. Tell me about a time you used analysis to make a recommendation.

- **Situation:** In the PLP PesaPap growth-analytics project, the team needed to decide whether an onboarding experiment showed a meaningful conversion difference.
- **Task:** Compare the variants accurately and make a recommendation without overstating what the generated data could prove.
- **Action:** I used SQL/SQLite and pandas to validate and analyse the experiment, calculated conversion rates, and used a chi-square test with a 95% confidence interval. I separated the conversion result from revenue and downstream payment outcomes, which the synthetic data did not establish.
- **Result:** Variant B converted 13.81% versus 10.46% for A, a 3.34 percentage-point observed difference (p = 0.0052; 95% CI 1.00–5.67 pp). I recommended a phased rollout with a persistent holdout and downstream activation and retention guardrails. The result applies only to the synthetic experiment.

### 2. Tell me about a time you identified a data-quality issue.

- **Situation:** While building lifecycle analyses for the PesaPap project, some generated transactions were dated before the associated user's signup.
- **Task:** Prevent impossible event timing from distorting cohort and customer-lifecycle measures while keeping the source data auditable.
- **Action:** I wrote a validation query to count pre-signup transactions, preserved the original records, and excluded those events from lifecycle RFM and cohort activity rather than silently deleting or crediting them.
- **Result:** The validation surfaced 3,737 pre-signup transactions. Overall transaction totals remain clearly distinguished from lifecycle metrics, and the README documents the treatment. This is a data-quality limitation in a synthetic dataset, not an observed production incident.

## Practice

Keep answers concise: explain the decision, method, result, and limitation. Replace these project examples with workplace examples where relevant, and be ready to walk through the notebooks and SQL queries.
