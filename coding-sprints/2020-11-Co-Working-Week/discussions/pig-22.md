# PIG 22
Tuesday Nov. 24th, 16h30


### Overview
A few preliminary comments from Axel: I guess the question is how far we want to go with the unification. I think in the most general case one could reduce to the following classes:
- `FluxPoints`, which would be generalised to handle time bins and regions as well. It would then offer convenience methods like `.plot_lightcurve(energy=)` or `.plot_profile()`, or `.get_flux_points(source=, time=, idx=)` or similar
- `FluxMap` basically as implemented here: https://github.com/gammapy/gammapy/pull/3075
- `FluxPointsEstimator`, which would be extended to handle `time_intervals` and regions as well
- `ExcessPointsEstimator`, implements the Li&Ma solution for the points. The code is basically already there as `ExcessProfileEstmator`
- `TSMapEstimator` could be renamed to `FluxMapEsimator`, `ExcessMapEstimator` stays as is.
- Both `FluxPointsEstimator` and `ExcessPointsEstimator` would return a `FluxPoints` object, and the map estimators a `FluxMap` object respectively...
- `LightCurveEstimator` and `ExcessProfileEstimator` would be removed...


### Notes
- FluxMap is useful, implements I/O and convenience to extract flux points
- Store the reference model as `SpectralModel`, on "data import", users have to define a model or we assume 
- Régis: use a "flattened" table to store combined time / energy and rely on Astropy's grouping of tables
- Internally always use the norm / likelihood format and and expose the `sed_type` in `.plot()` or `.write_table()`
- Generalise `FluxPoints` object, either by array columns or the flattened data structure mentioned above
- Generalise `FluxPointsEstimator` to handle `time_intervals` or `regions`?
- For `Excess` estimators one would store the excess directly, but we have to clarify which information to store if there is no exposure / flux estimate available
- For v1.0 try to have the final API design and rather leave certain functionality un-implemented
