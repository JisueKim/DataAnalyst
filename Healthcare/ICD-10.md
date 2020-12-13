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

https://realpython.com/pandas-dataframe/
https://rfriend.tistory.com/487
https://github.com/bryand1/icd10-cm

