# peaks-time-series
 Finds the peaks and stationary points and intervals of a time series data.


## What it does
 The function `get_peaks()` takes the time series data as an input and returns a pandas dataframe with points of interest which by default includes points where there is a sudden dip or sudden rise in the time series. The function can also return points where the time series is stationary by specifing a True value to the `return_stationary` parameter.


 The function acomplishes this using exonential smoothing and concepts from differential calculus. You can change how strict the function is when finding these points by changing the `strictness_level` parameter that takes values of 1, 2 or 3. The higher the value, the more strict the model will be in selecting these points.

 ## `get_peaks()` Parameters

 -`data` : The only required parameter. This is the source of the data where the time series is located. Must be a .csv or a .txt file containing comma seperated values.

 -`strictness_level` : The higher it is, the more strict the model will be. If it does not lie between 1 and 3, then the default parameters will be set as if `strictness_level` is 2, however these parameters can be altered individually if that is the case. Parameters that are affected by this parameter include: `percentile, rolling_window, num_points` and `stationary_slope`. Default 0.
 
 -`time_series_col`:  Defaults to 'Wl-Depth'


-`make_plot`: If True, the function will make a plot with the original time series and the points of interest found by the model. Default True.

-`display_statistics`: If True, the function will display a table of basic statistics of the original time series which include count, mean, standard deviation, min, max and quartiles. Default False.

-`only_return_point_type`: If True, the dataframe returned by the function will only include the Point type column of the dataframe without any added columns that were used to find that point type. If False, the function will return the dataframe with the first and second difference of the time series as well as the rolling window absolute maximum on the second difference that was used to find the vertices. Default True

-`return_stationary`: If True, the function will return points in the time series where it was remaining at a same level. Default False.

 -`smooth_factor`: The factor to be used to smooth the `time_series_col` Default 0.1

-`smooth_diff_factor`: The factor to be used to smooth out the first and second level differences of the `time_series_col`. Default 0.04 

-`percentile` : The percentile used to find the biggest values in the second difference column. If set too low, the model will identify more vertices, if set too high, the model will be more selective in which points to select as vertices. Default 0.75

-`rolling_window` : The size of the rolling window used to get the rolling window absolute maximum second difference column. If set too high, vertices close to one another will be identified, if set too low, neighboring vertices will be ignored. Default 200.

-`group_time_freq` : The time frequency in which the model will group neighboring points to a single point. Use `xS` to group for x amount of seconds, for example 5S wil be for 5 Seconds. Use `xT` for x amount of minutes. Default 'T'

-`num_points` : The minimum amount of consecutive stationary points in order to be considered as a stationary interval in the time series. The higher the value, the less likely is to find stationary intervals.Default 30.

-`stationary_slope` : The maximum absolute value the slope (first difference) of the time series must be in order to be considered as stationary. The higher the value, the less likely to find stationary points. Default 0.01.
 

