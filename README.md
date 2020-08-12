# super-umbrella
## Semi-automated BET analysis!

To produce a BET area for a given adsorption isotherm, in a semi-automated fashion, you can use this python code.

The code requires Python 3.6 or later and uses the packages numpy, scipy, matplotlib and pandas.

The code is stored in the python script **generateBET.py** and an example calculation is demonstrated for the isotherm *R*. The analysis produces graphs of the isotherm, consistency criteria and a comma-separated values (CSV) file of results from the linear regression.

The criteria from Rouquerol et al. [10.1016/S0167-2991(07)80008-5](https://doi.org/10.1016/S0167-2991(07)80008-5) are implemented in the following way:
- The quantity "ads_amount*(1-pp0)” is evaluated. This is then analysed to find the pp0 region where this quantity is increasing (simply based from the maximum value).
- The pp0 region of the isotherm is then cropped to the region defined above.
- For each consecutive three points the slope of the BET equation is calculated and recorded only if is linear (based on the r2 value), intercept > 0 and c-value > 0.
- The pp0 monolayer coverage is then compared to the pp0 region used to calculate the BET area.

When there are many points where the pp0 monolayer coverage is within pp0 region the greater surface area is taken (usually corresponding to higher pp0). If the Rouquerol criteria is not fulfilled by any points, usually because the pp0 monolayer coverage is not within the pp0 region, then the closest region is taken with greatest surface area.

The final BET area value should be compared to the variation of BET area for all the pp0 regions, to ensure it does not correspond to an outlier.

