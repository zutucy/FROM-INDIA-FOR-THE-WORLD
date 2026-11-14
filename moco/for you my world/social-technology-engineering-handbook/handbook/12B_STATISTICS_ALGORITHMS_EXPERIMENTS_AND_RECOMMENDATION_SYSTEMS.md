# 12B — Statistics, algorithms, experiments and recommendation systems

## 1. Why statistics matters

Products produce observations: views, clicks, orders, errors, searches, watch time and support reports. Observations are not proof that a change caused an outcome. Statistics helps distinguish signal from noise, quantify uncertainty and avoid decisions from anecdotes.

Start with a question: “Did the new onboarding improve activation?” Define activation before looking at results. Choose the eligible population, time window, primary metric, guardrails and minimum practical effect.

## 2. Core statistical ideas

- **Population/sample:** The group of interest versus the observed subset.
- **Mean/median:** The mean is sensitive to extremes; median often better describes skewed latency or spending.
- **Variance/standard deviation:** Spread around a central value.
- **Correlation/causation:** Two variables moving together does not prove one caused the other.
- **Confidence interval:** A range from a method with stated long-run coverage; it is not simply a probability that a fixed parameter lies in this one observed interval.
- **Statistical/practical significance:** A tiny effect can be statistically detectable at huge scale and still not be worth the cost.
- **Selection and survivorship bias:** The observed sample may systematically exclude relevant users or failures.
- **Simpson's paradox:** Aggregated trends can differ from within-group trends.

Avoid searching many segments until one looks favourable. Predefine primary outcomes for high-risk experiments.

## 3. Algorithms before machine learning

An algorithm is a finite procedure to solve a problem. It may use rules, sorting, graph traversal, search, ranking or optimization. Many production systems combine these with learned models.

Important structures and ideas: arrays, hash maps, sets, trees, heaps, graphs, sorting, searching, breadth-first/depth-first traversal, shortest paths, greedy methods, dynamic programming, and time/space complexity using Big-O notation.

A social graph illustrates the connection between algorithm and storage: finding followers needs a suitable index and query direction; finding friends-of-friends may create a large fan-out and needs bounded depth/filters.

## 4. Recommendation pipeline

A recommender is usually a pipeline, not one mysterious AI model:

1. Candidate generation: retrieve a manageable pool.
2. Eligibility filtering: remove private, blocked, deleted, unavailable or policy-violating items.
3. Feature computation: calculate permitted signals.
4. Ranking: estimate relevance for a defined objective.
5. Re-ranking: apply diversity, freshness, creator exposure and repetition constraints.
6. Serving: return a bounded page with pagination/caching.
7. Feedback: capture impressions, skips, hides, reports and interactions.
8. Evaluation: measure quality, user outcome, safety and long-term effects.

Privacy and policy eligibility must be enforced before serving, not left to the ranking model.

## 5. Signals and bias

Possible signals include follows, declared interests, search terms, saves, shares, completion, freshness, language and negative feedback. Each has manipulation, bias and privacy implications. An impression matters: a non-click on content never seen is not rejection. Logging only clicks creates exposure bias. Position also affects opportunity.

Use purpose-limited signals and document them. Avoid sensitive-attribute inference without clear necessity and lawful basis. Offer meaningful controls where practical: chronological view, not-interested, mute, block and topic preferences.

## 6. Objective design and unintended effects

Maximizing watch time can reward sensational content; maximizing clicks can reward misleading titles; maximizing comments may reward conflict. Use balanced objectives and guardrails: user-reported satisfaction, task success, relevance, freshness, creator/topic diversity, negative feedback, safety outcomes, language coverage, latency and cost.

Maintain a simple chronological or rule-based baseline. Complexity must earn its operational cost with measured improvement.

## 7. A/B testing

Randomized experiments compare variants under design assumptions. Define hypothesis, eligible population, assignment unit, primary metric, guardrails, sample size, duration and rollback criteria. Check instrumentation and sample-ratio balance. Avoid stopping early because a temporary p-value looks good. Consider seasonality, novelty, long-term outcomes and interference between users. Network products may need cluster/geographic experiments because one person's treatment affects another.

A/B tests do not prove a feature is ethical or safe. Combine quantitative outcomes with qualitative research and post-launch monitoring.

## 8. Trending and discovery

Trending is not merely the largest total count. Raw totals favour old and large accounts. Consider recency, rate relative to baseline, unique participants, quality, spam anomalies and diversity. Coordinated manipulation is possible; combine automated signals with reporting and human escalation for high-impact trends.

## 9. Evaluation

Classification may use precision, recall, F1, ROC-AUC or PR-AUC depending on class imbalance and error cost. Ranking may use NDCG, MAP or MRR. Offline metrics need online and human evaluation. In moderation, false negatives allow harm; false positives suppress legitimate content. Aggregate scores can hide poor language/region performance.

## 10. Exercise

Build a rule-based recommender over toy records. Generate candidates from followed authors and declared interests; filter private/blocked items; rank by freshness and topical relevance; enforce a diversity cap. Compare with chronological order and write down what your metric fails to measure.

## Sources

- Google Rules of ML: https://developers.google.com/machine-learning/guides/rules-of-ml
- Google ML Crash Course: https://developers.google.com/machine-learning/crash-course
- Wide & Deep recommender paper: https://research.google/pubs/wide-deep-learning-for-recommender-systems/
- NIST AI RMF: https://www.nist.gov/itl/ai-risk-management-framework
