# Prompt Regression Testing: Preventing Quality Decay - Statsig

- URL: https://www.statsig.com/perspectives/slug-prompt-regression-testing
- Type: article
- Published: unknown
- Topic: evals

Describes prompt regression testing as an assertion-based, version-pinned practice run in CI on every pull request, analogous to unit testing but with rubric-floor assertions (e.g., groundedness >= 0.85) instead of string equality checks.
Outlines patterns including per-rubric assertion, per-route stratified evaluation, and paired comparison against a prior prompt version with a CI-reported score delta.
