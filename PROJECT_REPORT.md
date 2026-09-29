# Stock Market Price Prediction Using Machine Learning

## Internship minor project report

Student: Singarapu Tirumala Raja Vardhan
Institution / department: Annamacharya University / AI&DS Department  
Internship organization / mentor: Corizo edu.Tech

## Abstract
This project studies next-observation price prediction for AMZN, DPZ, NFLX and BTC using 1,520 historical records from 1 May 2013 to 14 May 2019. It compares Ridge regression and Random Forest regression against a persistence baseline. Causal return and rolling-window features, chronological partitions and validation-only model selection support a reproducible evaluation. BTC is a cryptocurrency, included as a separate asset in the supplied file. Predictions are historical experiments, not current market forecasts.

## Problem statement
Given the prices observed up to an origin date, estimate the price at the next recorded date. The project tests whether machine learning reduces out-of-sample price error relative to simply repeating the current price.

## Dataset and provenance
The supplied CSV has Date, AMZN, DPZ, BTC and NFLX columns. There are no missing values or duplicate dates in the evaluated input. The user identifies it as Kaggle data; the original URL, license, currency and adjustment conventions are not available. Add the original Kaggle citation before submission. A SHA-256 checksum is saved in results/data_audit.json. Dates absent from the file are not imputed. This is particularly relevant to BTC, which normally has a different observation calendar from equities.

## Methodology
1. Parse dates, sort and validate numeric positive prices.
2. Visualize normalized price paths and correlations between observed returns.
3. Engineer 15 features per asset: six return lags, plus momentum, moving-average ratio and volatility over 5, 10 and 20 observations.
4. Predict next return; reconstruct next price from the current price.
5. Split usable origins into approximately 70% training, 15% validation and 15% test, purging one origin at each boundary. Each asset has 1,499 usable labeled rows before these two purges.
6. Compare persistence, three Ridge regularization settings and two Random Forest leaf sizes. Ridge uses a training-fitted standardization pipeline. Forests use 150 trees, depth at most 8 and random seed 42.
7. Select each family's configuration and the overall model using validation RMSE. Refit on pre-test data and evaluate on the held-out test period without further selection.
8. Refit the validation-selected configuration on all labeled historical data for a separate unscored next-observation inference example.

The evaluation predicts one step at a time using actual prices available at each origin, while model parameters stay fixed through the test period. It does not predict the entire test path from a single initial observation.

## Results
Price errors use the dataset's unspecified price units. Positive RMSE reduction indicates improvement over persistence; negative values indicate deterioration. The selected model is chosen using validation, not the test results.

| Asset | Validation-selected model | Test MAE | Test RMSE | Persistence RMSE | RMSE reduction |
|---|---|---:|---:|---:|---:|
| AMZN | Ridge alpha=1.0 | 27.6854 | 38.7120 | 38.5079 | -0.53% |
| DPZ | Ridge alpha=100.0 | 3.9496 | 5.0792 | 5.0695 | -0.19% |
| BTC | Persistence | 138.5141 | 223.6568 | 223.6568 | 0.00% |
| NFLX | Ridge alpha=1.0 | 7.1380 | 9.3462 | 9.2955 | -0.54% |

Full metrics for all three model families, including MAPE, R² and directional accuracy, are included in results/test_metrics.csv. Do not describe R² as a percentage of correct forecasts. Direction accuracy treats unchanged as a third category, so persistence is not a coin-flip direction benchmark.

## Discussion
Small improvements on a single period are not evidence of a reliable trading advantage. Where persistence wins or the validation-selected ML model performs worse on test, report that outcome directly. Stock price levels can look very accurately predicted because successive prices are close even when returns are difficult to forecast. A strong baseline is therefore essential.

## Verification
The notebook executed fully without error. Assertions verify the input schema and values, chronology, strict separation between label dates and subsequent partition origins, feature invariance when future data is removed, finite evaluation metrics and one validation-selected model per asset. These checks establish experiment consistency, not market profitability.

## Limitations
The dataset is historical and small, with unverified price-field semantics and no volume, news or corporate-action metadata. A single split may be sensitive to market regime. No live deployment, transaction-cost analysis, trading strategy or calibrated uncertainty intervals were evaluated. The final inference example is anchored at 14 May 2019 and has no known target in this CSV.

## Future scope
Verify dataset provenance and licensing; add current adjusted data with explicit timestamps; perform expanding-window validation across regimes; compare return errors; test temporal uncertainty calibration; and assess economic value only with a properly specified cost-aware backtest.

## Conclusion
This project delivers an end-to-end, reproducible ML forecasting experiment with honest baseline comparisons. Its value is the complete methodology and measured results, including evidence that added model complexity may not improve prediction.

## References and attribution
- User-supplied portfolio_data.csv; original Kaggle dataset reference to be added by the student.
- Python libraries and exact tested package versions are listed in requirements.txt.
- Consult the notebook's viva-preparation section for explanations of the experimental choices.
