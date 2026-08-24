# Operator

Select from the following:

| Operator | Impact on results | Remark |
| :-- | :-- | :-- |
| _blank_ | No change to result. |  |
| + | The value of either the [Constant](./constant.md) or [Pay Counter](./pay-counter.md) is **added** to the result. | _Constant_ has priority over _PayCounter_. Also see below (a) |
| \- | The value of either the [Constant](./constant.md) or [Pay Counter](./pay-counter.md) is **subtracted** from the result. | _Constant_ has priority over _PayCounter_. Also see below (a) |
| \* | The value of either the [Constant](./constant.md) or [Pay Counter](./pay-counter.md) is **multiplied** to the result. | _Constant_ has priority over _PayCounter_. Also see below (a) |
| / | The value of either the [Constant](./constant.md) or [Pay Counter](./pay-counter.md) is **devided** to the result. | _Constant_ has priority over _PayCounter_. Also see below (a) |
| Round down | Rounds the result **down** to the precision of the [Constant](./constant.md). | _Pay Counter_ not in use. |
| Round up | Rounds the result **up** to the precision of the [Constant](./constant.md). | _Pay Counter_ not in use. |
| Minimum | The result is set to at least the value of the [Constant](./constant.md). | Only apply Minimum if result until now is >0. Also see below (a) |
| \= | The result is set to the value of the [Constant](./constant.md). | _Pay Counter_ not in use. |

1.  If both _Constant_ **and** _Pay Counter_ are present - the _Constant_ is only used if the value of _Pay Counter_ are <> 0.

Also see the possibility for [enable troubleshooting](./debug-pay-type-formula.md).
