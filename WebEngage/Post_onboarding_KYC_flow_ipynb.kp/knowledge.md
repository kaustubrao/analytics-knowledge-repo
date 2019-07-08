---
title: Analysis of KYC flow of onboarded users - from submission of KYC Docs to KYC
  Approval
authors:
- Kaustub
tags:
- knowledge
- example
created_at: 2019-07-08 00:00:00
updated_at: 2019-07-08 18:22:03.392260
tldr: 32% of onboarded users submit their KYC Docs at least once, 18% of these users
  get approved, 13% are rejected, and 70% are asked to resubmit, 55% of the users
  asked to resubmit will resubmit at least once
---

### Motivation

- To set benchmarks for KYC activity of users targeted through WebEngage

### 32% of users will submit KYC Docs at least once


```python
import pandas as pd
df = pd.read_csv('/Users/kaustub/analytics-knowledge-repo/WebEngage/kyc_flow.csv')
df.drop_duplicates(inplace=True)
percentiles=[.01,.05,.1,.2,.3,.4,.5,.6,.7,.8,.9,.95,.99]
print("% Submitted KYC Docs : {:,.1%}".format(len(df[~(df.kyc_sub_date.isna())])/len(df)))

```
    % Submitted KYC Docs : 31.7%


### 80% of these users will submit Docs within 3 days of onboarding


```python
kyc_subs = df[~(df.kyc_sub_date.isna())]
print("Distribution of days to KYC submission")
#print("")
pd.DataFrame(kyc_subs.days_to_kyc_sub.describe(percentiles=percentiles)).style.format('{:,.0f}')
```
    Distribution of days to KYC submission






<style  type="text/css" >
</style><table id="T_9884ad42_a17a_11e9_a759_d0817ac8b878" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >days_to_kyc_sub</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row0" class="row_heading level0 row0" >count</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row0_col0" class="data row0 col0" >16,822</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row1" class="row_heading level0 row1" >mean</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row1_col0" class="data row1 col0" >10</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row2" class="row_heading level0 row2" >std</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row2_col0" class="data row2 col0" >35</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row3" class="row_heading level0 row3" >min</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row3_col0" class="data row3 col0" >-61</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row4" class="row_heading level0 row4" >1%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row4_col0" class="data row4 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row5" class="row_heading level0 row5" >5%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row5_col0" class="data row5 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row6" class="row_heading level0 row6" >10%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row6_col0" class="data row6 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row7" class="row_heading level0 row7" >20%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row7_col0" class="data row7 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row8" class="row_heading level0 row8" >30%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row8_col0" class="data row8 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row9" class="row_heading level0 row9" >40%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row9_col0" class="data row9 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row10" class="row_heading level0 row10" >50%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row10_col0" class="data row10 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row11" class="row_heading level0 row11" >60%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row11_col0" class="data row11 col0" >0</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row12" class="row_heading level0 row12" >70%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row12_col0" class="data row12 col0" >1</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row13" class="row_heading level0 row13" >80%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row13_col0" class="data row13 col0" >3</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row14" class="row_heading level0 row14" >90%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row14_col0" class="data row14 col0" >20</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row15" class="row_heading level0 row15" >95%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row15_col0" class="data row15 col0" >68</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row16" class="row_heading level0 row16" >99%</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row16_col0" class="data row16 col0" >199</td>
            </tr>
            <tr>
                        <th id="T_9884ad42_a17a_11e9_a759_d0817ac8b878level0_row17" class="row_heading level0 row17" >max</th>
                        <td id="T_9884ad42_a17a_11e9_a759_d0817ac8b878row17_col0" class="data row17 col0" >316</td>
            </tr>
    </tbody></table>