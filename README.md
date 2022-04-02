# Allocator

_Currently, the source code for this project is private. It will be made available once retired for public use. When public, the code will be available on this [GitHub repository](https://github.com/preritdas/allocator)._

----

Allocator is an automated portfolio manager that constantly rebalances holdings to match a pre-defined sectoral division. For example, an allocation in `main.py`'s global parameters might look like:

```python
allocation = {
    "Domestic Large Cap": 0.35,
    "Domestic Mid Cap": 0.05,
    "Domestic Small Cap": 0.02,
    "International": 0.18,
    "Short Term Bonds": 0.12,
    "Aggregate Bonds": 0.28
}
```

Every day, Allocator will read the available cash balance and invest in various ETFs such that the account is exposed to the market in as close to the `allocation` as possible. 

Depositing cash consistently to the account after deployment is _encouraged_ (but not necessary), as this is what gives Allocator the ability to re-invest in all sectors.

Allocator submits several fractional orders to ensure that it can achieve a balance as close as possible to the predefined `allocation`. To ensure rapid execution, when purchases are necessary, allocator will designate the order execution task for each ETF to an independent CPU core. This allows orders to be submitted concurrently and rapidly. 

## Upcoming Features

These are not fully developed yet and are not part of the `main.py` deployment.

### Rebalancing by Sale

Allocator will be able to periodically check on the account's market exposure and sell various positions to keep it near-perfectly in line with the predefined `allocation`. Currently, it only purchases ETFs according to the `allocation`, which theoretically should maintain optimal exposure, but small deviations compound over time which is why a watchdog protocol is necessary for continual deployment.