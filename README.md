
### Notice

This repository only contains the documentation of warp10-ext-forecasting.

The documentation is located under `doc/`.

These functions are available on the Warp 10 instance of the sandbox.

To install this extension on your own instance, you can contact us.

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
AUTO                 // automatically choose a forecast model (include all of the above but ignore seasonal component)
</pre>

Functions that take a GTS forecast model as argument:
<pre>
FORECAST                 // forecast values in the future
FORECAST.ADDVALUES       // forecast values in the future and append them to observation GTS
INFORECAST               // produce in-sample one-step ahead forecasts
CROSSFORECAST            // forecast values given a model fitted with another GTS
CROSSFORECAST.ADDVALUES  // forecast values given a model fitted with another GTS and append them to input GTS
FORECAST.ANOMALIES       // detect anomalies in in-sample forecast
FORECAST.ANOMALIES.DROP  // detect anomalies in in-sample forecast and drop them from input GTS    
MODELINFO                // return map of information about the model
AIC                      // compute Akaike information criterion
</pre>

Functions related to stationarity and differencing:
<pre>
STATIONARY     // test whether input GTS is stationary
DIFF           // apply time differencing with one or more seasonalities
INVERTDIFF     // integrate with one or more seasonalities
</pre>

Fit / Transform / Inverse-Transform  programming pattern (similar to sklearn)
<pre>
FIT               // fit a GTS transformer
TRANSFORM         // transform a GTS using a GTS transformer
INVERSETRANSFORM  // inverse-transform a GTS using a GTS transformer
GTSTRANSFORMER    // build a GTS transformer from a set of macros
DIFFERENCER       // build a GTS transformer for time differencing
</pre>


#### Examples

`<GTS> AUTO 5 FORECAST` pushes onto the stack a GTS with 5 forecast ticks.

`<GTS> AUTO 5 FORECAST.ADDVALUES` merges a GTS with its forecast.

