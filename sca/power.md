Power
=====

This week we're going into basic attacks and information about power analysis and other power related information.

Levels of an attacker:
- passive
  - just listening and doing normal inputs
- active
  - doing things beyond the normal operation space to adversely affect it
- invasive
  - do anything. depackaging, direct contact, using a mill, etc.
- semi-invasive
  - depackaging could still occur, but we aren't modifying specific signals
- non-invasive
  - no permanant alterations

This course is non-invasive, passive attacking. Side channels are inherently passive since they're viewing leaked information.

Power consumption at any time is directly related to the data and functions/operations.

## Power Traces
What is in a power trace?

1. Operation dependant power ($$P_{op}$$).
2. Data dependant power ($$P_{data}$$).
3. Power from electronic noise ($$P_{noise}$$).
  - Assuming we run the same operation/data through a system repeatedly, the measurements will always be different due to electronic noise.
4. Power from other sources is the "constant source" ($$P_{const}$$).
  - The device has other operations occuring during the processing of our data.

The total power used on a device is the sum of these four power sources.

### Distributions
X ~ N(mu, sigma)
mu -> is mean
sigma -> is SD

If the power traces fall within some normal distribution, we cna then begin to model the system. That's the convergence we want.
- we would estimate the properties with x-bar and s^2 to be the estimates of mu and sigma respectively. 