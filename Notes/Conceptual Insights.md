Key Insights :

Understanding the project : 

This project is not about regime-shift or seasonal modeling problem. It is a noise-dominant dynamics project

AirPassengers dataset was didactic. The structure was strong, stable, and aligned with Holt–Winters’ assumptions. In that context, allowing optimization was not hiding failure; it was helping the model settle into a structure that genuinely existed.
However for Walmart,  the dataset is adversarial. The dominant characteristic is volatility, not structure. 

Understanding Need for detailed documentation : 

Documentation on Holts-Winter model’s glaring incapability in Section 2 to 4 : What you have just written is raw insight. In the README or final presentation, this will compress into three or four sharp paragraphs. But without doing this work, that compression would be hollow.

Understanding various Models : 

ARIMA answers “can short-term dependence be modeled once instability is removed?”
        ◦  For Project 2, the second question is the sharper contrast
        ◦ Holt–Winters asks:
“Can I smooth my way through instability by assuming the structure persists?”
        ◦ ARIMA asks:
“Can I remove instability first, and then model what remains?
If Holt–Winters failed because it assumed persistence, ARIMA is being tested because it questions persistence.

A regression-based model with calendar effects simply means this:You treat time as data, not as an evolving state, and you explain sales using explicit calendar variables instead of smoothing past values. To put it plainly: trend-only regression answers “is there a long-term direction?”

ML models introduce capacity before you have finished understanding the statistical failure modes. They can absorb volatility through flexibility, but they do not tell you why that volatility exists or whether it is signal or noise.

Intuitions and insights for Implementation : 

(1) Aggregation is not a trick to make data “behave.” It is a diagnostic choice made when turbulence at a fine scale prevents you from even answering the first-order question: is there any structure here at all? Once that question is answerable, the modeling path becomes clearer.

(2) Parameter optimization : When you allow optimization, the optimizer is no longer sharpening an existing signal; it will tend to manufacture explanations for noise.
To sum it up, Optimizing Holt–Winters parameters hides instability by smoothing it away; optimizing ARIMA orders hides instability by fragmenting it across parameters.
Simply put, Optimization answers “how good can this model look?” Diagnosis answers “should this model be trusted at all?”
Bottom line : we don’t use default function to optimize the parameters - alpha, beta and gamma (Holt-Winter), pqd (ARIMA) but take manual parameters in a conservative manner

(3) Purpose of parameters – Comparison :
In Holt–Winters, fixing alpha, beta, and gamma was about stress-testing a structural assumption. You were asking whether the data naturally supports stable level, trend, or seasonality without the model constantly re-correcting itself. The failure you observed was a mismatch between assumed structure and reality.
In ARIMA, fixing p, d, and q is about isolating memory behavior. You are asking whether short-range linear dependence exists at all, and if so, how quickly it collapses under volatility. Here, you are not testing structure but persistence. Any brittleness you observe is evidence that dependence is local, fragile, or episodic.
(4) Understanding ACF & PACF plots : Whenever there’s seasonality, the ACF often shows a taller spike at the seasonal lag (like 12 for monthly data) than the PACF, because the ACF captures both the direct and the indirect influence — all the “echoes” of that repeating cycle.

(5) Direction of Lags : A negative PACF at lag 1 means: After removing all other influences, there’s a direct negative link between this month and the previous month. A negative lag-1 PACF (or ACF) means:The second month tends to move opposite to the first month.

(6) In ACF and PACF plots, the very tall first bar you see everywhere at lag 0 is always there — it just represents “a series correlates perfectly with itself.” Every ACF/PACF plot has that; we ignore it when interpreting.

(7) Analysis of plots – to understand ARIMA better

ACF/PACF spikes before modeling (on differenced data) are good — they give the model something to learn.
ACF/PACF spikes after modeling  (residuals) are bad — they mean the model left structure behind.
Volatility clustering in residuals is also bad — it means risk is structured, not random.

(8) The general behavior of any ARMA(p, q) model — the shape stays similar even if the parameters are tweaked. Their interference may produce that gentle oscillation which we can see in ACF and PACF — a pattern that rises and dips a few times before settling down near zero.
