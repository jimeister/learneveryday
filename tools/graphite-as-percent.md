# asPercent instead of divideSeries

Instead of using `divideSeries` and `scale` to calculate percentages in [graphite](https://graphite.readthedocs.org/en/latest/), simply use `asPercent` instead.

Example:
```
asPercent(prod.mobile-fe.response.{5??,throw}.count, prod.mobile-fe.response.*.count)
```

Rather than:
```
scale(divideSeries(prod.mobile-fe.response.{5??,throw}.count, prod.mobile-fe.response.*.count), 100)
```

[reference](http://graphite.readthedocs.org/en/0.9.10/functions.html#graphite.render.functions.asPercent)
