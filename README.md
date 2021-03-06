
### Notice

This repository only contains the documentation of warp10-ext-forecasting.

The documentation is located under `src/main/warpscript/io.warp10/warp10-ext-forecasting/`.

These functions are available on the Warp 10 instance of the sandbox.

To install this extension on-premise or to make it available on your saas plan, please contact us.

### Forecast extension for the WarpScript language

Functions that build GTS forecast models:
<pre>
RANDOMWALK           // build a random walk model
SRANDOMWALK          // build a random walk model that is seeded with PRNG function
LSTM                 // build an LSTM neural network model
NNETAR               // build a neural network auto-regressive model
SES                  // build a simple exponential smoothing model
HOLT                 // build a Holt's linear model (SES + trend)
HOLTWINTERS          // build a Holt-Winters' model (SES + trend + seasonal)
ARMA                 // build an auto-regressive moving average model
ARIMA                // build an auto-regressive integrated moving average model
SARMA                // build a seasonal auto-regressive moving average model
SARIMA               // build a seasonal auto-regressive integrated moving average model
SEARCH.ETS           // search for a suitable exponential trend-seasonal model (include SES, HOLT and HOLTWINTERS)
SEARCH.ARIMA         // search for a suitable Arima model (include ARMA and ARIMA)
SEARCH.SARIMA        // search for a suitable Sarima model (include SARMA and SARIMA)
SEARCH.NNET          // search for a suitable neural network model (include LSTM and NNETAR)
AUTO                 // automatically choose a forecast model (non-seasonal), using AIC
SAUTO                // automatically choose a seasonal forecast model, using cross-validation
</pre>

Functions that uses a GTSFORECASTMODEL:
<pre>
FORECAST                 // forecast values in the future
FORECAST.ADDVALUES       // forecast values in the future and append them to observation GTS
INFORECAST               // produce in-sample one-step ahead forecasts
CROSSFORECAST            // forecast values given a model fitted with another GTS
CROSSFORECAST.ADDVALUES  // forecast values given a model fitted with another GTS and append them to input GTS
FORECAST.ANOMALIES       // detect anomalies in in-sample forecast
FORECAST.ANOMALIES.DROP  // detect anomalies in in-sample forecast and drop them from input GTS
</pre>

Functions that gives info on a GTSFORECASTMODEL
<pre> 
MODELINFO                // return map of information about the model
OBSERVATIONS             // observation GTS used for fitting the model
AIC                      // Akaike information criterion
AICC                     // corrected Akaike information criterion
BIC                      // bayesian information criterion
NPAR                     // number of parameters
LOGLIKELIHOOD            // estimated log-likelihood
</pre>

Functions related to stationarity and differencing:
<pre>
STATIONARY     // test whether input GTS is stationary
SEARCH.FOR.D   // search for the number of times a GTS needs differencing to become stationary
DIFF           // apply time differencing with one or more seasonalities
INVERTDIFF     // integrate with one or more seasonalities
DIFFERENCER    // build a GTS transformer for time differencing
</pre>

Fit / Transform / Inverse-Transform  programming pattern (similar to sklearn)
<pre>
GTSTRANSFORMER    // create a GTS transformer from a set of macros
FIT               // fit a GTS transformer
TRANSFORM         // transform a GTS using a GTS transformer
INVERSETRANSFORM  // inverse-transform a GTS using a GTS transformer
</pre>


#### Examples

`<GTS> AUTO 5 FORECAST` creates a GTS containing the 5 forecast ticks using an automatically selected model.

`<GTS> AUTO 5 FORECAST.ADDVALUES` merges a GTS with its forecast.

`<GTS> 24 SAUTO 48 FORECAST` creates a GTS containing the 48 forecast ticks using a model considering that there is a 24-tick seasonal cycle.

`NEWGTS RANDOMWALK 1000 FORECAST` populates a new GTS with random walk

#### Recommendations and troubleshooting

The input GTS needs not be bucketized and filled, but it will work better if it is the case.

Each next forecast will be on tick = last_tick + (last_tick - penultimate_tick).

Use UNBUCKETIZE first if the last bucket does not match the tick of the last non-null value, or else there will be a gap between the last non-null value and the first forecast value.

The forecast functions have an optional argument that defines the maximum number of past ticks they use to build their model (max input size). The default value is dependent on the model so that their default time to execute is roughly equivalent.
