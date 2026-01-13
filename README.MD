1. Problem Framing 

The Walmart dataset was used for this project. It contains daily transaction-level data spanning four years. The data was aggregated to a monthly level so that we could analyze overall demand behavior while smoothing out day-to-day and week-to-week fluctuations.
The resulting trend chart showed strong volatility and weak structure. There was no visually stable trend or seasonality, which suggested that Walmart demand might be driven more by shocks and regime changes than by smooth temporal patterns.

2. Why Holt–Winters Was Chosen First

Holt–Winters was chosen first because it explicitly assumes that a time series is driven by persistent components such as level, trend, and seasonality. In this project, Holt–Winters was used as a diagnostic tool to test whether such structure actually exists in Walmart data.
When applied to Walmart, Holt–Winters failed to produce stable or interpretable components. Whether parameters were optimized or fixed manually, the model repeatedly chased volatility rather than learning stable patterns. This demonstrated that when variance overwhelms structure, fixed-parameter smoothing models lose both interpretability and stability.

3. Why ARIMA Was Chosen as a Contrast

ARIMA was chosen as a contrast because it approaches time series from a fundamentally different philosophy. Instead of decomposing data into components, it removes non-stationarity through differencing and then looks for linear dependence through lagged relationships.
Rather than assuming persistence, ARIMA tests whether the present can be explained by the recent past. Instead of learning trend and seasonality, it learns correlations.

4. What ARIMA Revealed

After differencing, the Walmart series remained highly volatile, showing that while the trend was removed, the data-generating process was still dominated by irregular shocks rather than smooth structure. This indicates that Walmart demand has weak in-sample linear memory, leaving ARIMA with very little reliable dependence to exploit.
ACF and PACF of the differenced series confirmed this. Almost all spikes lie within the confidence bands, with only small and isolated excursions that do not form a meaningful decay or cutoff pattern. This shows that once the mean drift is removed, the series contains almost no stable linear autocorrelation.
The residuals provide the most important diagnostic. They are centered around zero, so the mean has been modeled, but their magnitude varies in clusters, with periods of calm followed by bursts of large errors. This volatility clustering shows that while ARIMA absorbed what little mean structure exists, the uncertainty itself is time-dependent. The errors are not identically distributed over time, confirming that Walmart demand is driven by regime changes and shocks rather than by stable patterns.

5. What Makes Walmart Adversarial

Walmart is a classic adversarial time series. It has no stable trend, no stable seasonality, and no meaningful linear memory in the form of autocorrelation or lag structure. The dominant property is clustered volatility.
This kind of behavior cannot be captured by classical smoothing models, which rely on stable components and small, random noise.

6. Business Implications

In this kind of scenario, the primary challenge is not accurate point prediction but risk and regime management. Business value comes from understanding how volatility changes over time, how extreme outcomes arise, and how demand behaves across different regimes.
For adversarial data, forecasting should focus on distributions, scenarios, and uncertainty rather than single-value predictions. In such systems, managing risk is more important than chasing accuracy.
