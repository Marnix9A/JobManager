# Calc. Method

| Option | Description |
| :-- | :-- |
| Time Comsump | The calculated net time for each registration, will be the weight when time allocation is performed. |
| Calculated Time Consump | The estimated time for each job task, will be the weight when time allocation is performed. |

If the job bundle contains mixed job types (e.g. _Production_ and _Job_), allocation _Time Consumption_ is used.

It the field [Bundle Factor](../general-setup/bundle-factor.md) assuming a value, this value will be used as an additional factor in the time allocation.

# Example

             TOTAL BUNDLE                (115 minuts)

                Break (10 minuts)

              JOB 1               (95 minuts)

       JOB 2    (30 minuts)

                             JOB 1     (35 minuts)

| Bundle Gross Time | Break | Bundle Net Time |
| --: | --: | --: |
| 115 | 10 | 105 |

# Time Comsump

### Formula = ((Job Registration / Total Job Registration) \* Bundle Net Time)

|  | Registration (X) | Formula | Result |
| :-- | --: | :-- | :-: |
| JOB 1 | 95 | ((95 / 160) \* 105) | **62.34** |
| JOB 2 | 30 | ((30 / 160) \* 105) | **19.69** |
| JOB 3 | 35 | ((35 / 160) \* 105) | **22.97** |
| **Total Job Registration** | **160** |  |  |

**(X) If [Bundle Factor](../general-setup/bundle-factor.md) is filled in on [the job](../general-setup/jobmanager-job.md), this is multiplied to the time for job registration.**

# Calculated Time Consump

### Formula = ((Job Registration / Total Calculated Time Consump) \* Bundle Net Time)

|  | Calculated Time Consump (X) | Formula | Result |
| :-- | --: | :-- | :-: |
| JOB 1 | 100 | ((100 / 175) \* 105) | **60.00** |
| JOB 2 | 30 | ((30 / 175) \* 105) | **18.00** |
| JOB 3 | 45 | ((45 / 175) \* 105) | **27.00** |
| **Total Calculated Time Consump** | **175** |  |  |

**(X) If [Bundle Factor](../general-setup/bundle-factor.md) is filled in on [the job](../general-setup/jobmanager-job.md), this is multiplied to the time for job registration.**
