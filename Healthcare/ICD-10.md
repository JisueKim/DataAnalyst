# ICD-10 CM 
ICD-10 is the 10th revision of the International Statistical Classification of Diseases and Related Health Problems (ICD), a medical classification list by the World Health Organization (WHO). It contains codes for diseases, signs and symptoms, abnormal findings, complaints, social circumstances, and external causes of injury or diseases.

## Getting Started


```python
!pip install icd10-cm
```


## Common Usage


```python
import icd10

code = icd10.find("J20.0")
print(code.description)         # Acute bronchitis due to Mycoplasma pneumoniae
if code.billable:
    print(code, "is billable")  # J20.0 is billable

print(code.chapter)             # X
print(code.block)               # J00-J99
print(code.block_description)   # Diseases of the respiratory system
```

    Acute bronchitis due to Mycoplasma pneumoniae
    J20.0 is billable
    X
    J00-J99
    Diseases of the respiratory system


### Check if an ICD-10 code exists


```python
import icd10

if icd10.exists("J20.0"):
    print("Exists")
```

    Exists


## Chapters

![ICD-10.png](https://github.com/JisueKim/DataAnalyst/blob/master/images/ICD-10.png?raw=true)

<style  type="text/css" >
    #T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391 th {
          text-align: left;
    }#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row0_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row0_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row0_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row1_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row1_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row1_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row2_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row2_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row2_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row3_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row3_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row3_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row4_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row4_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row4_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row5_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row5_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row5_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row6_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row6_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row6_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row7_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row7_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row7_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row8_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row8_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row8_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row9_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row9_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row9_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row10_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row10_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row10_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row11_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row11_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row11_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row12_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row12_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row12_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row13_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row13_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row13_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row14_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row14_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row14_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row15_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row15_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row15_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row16_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row16_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row16_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row17_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row17_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row17_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row18_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row18_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row18_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row19_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row19_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row19_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row20_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row20_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row20_col2,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row21_col0,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row21_col1,#T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391row21_col2{
            text-align:  left;
        }</style><table id="T_d9ad2d58_3c56_11eb_a3ab_3e22fbb86391" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Chapter</th>        <th class="col_heading level0 col1" >Block</th>        <th class="col_heading level0 col2" >Title</th>    </tr></thead><tbody

https://realpython.com/pandas-dataframe/
https://rfriend.tistory.com/487
https://github.com/bryand1/icd10-cm

