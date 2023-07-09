# Risk analysis
I calculated credit risk RWA and capital requirement for the bank's portfolio. I have to use data from the file [Loan default](https://github.com/uzhegovaelena/riskanalysis/blob/main/Loan%20default.xlsx) which contains loans with a status indicator: defaulted(bad) or non-defaulted. 

Here is short description of data columns:
- BAD: 1 = applicant defaulted on loan or seriously delinquent; 0 = applicant paid loan.
- LOAN: Amount of the loan request.
- MORTDUE: Amount due on existing mortgage.
- VALUE: Value of current property.
- REASON: DebtCon = debt consolidation; HomeImp = home improvement.
- JOB: Occupational categories.
- YOJ: Years at present job.
- DEROG: Number of major derogatory reports.
- DELINQ: Number of delinquent credit lines.
- CLAGE: Age of oldest credit line in months.
- NINQ: Number of recent credit inquiries.
- CLNO: Number of credit lines.
- DEBTINC: Debt-to-income ratio.

I used metrics such as:
- LTV: Loan-to-Value ratio. This is the ratio of the loan amount to the appraised value of the property or asset being financed. It is expressed as a percentage.
- EAD: Exposure at Default. This is the estimated value of the outstanding loan or credit line at the time of default. This can be done using statistical models or historical data.
- RW: Risk Weight. This is the weight assigned to a specific asset or loan based on its level of risk.
- RWA: Risk Weighted Assets. This is the amount of capital that a bank or financial institution must hold to cover potential losses due to credit risk. It is calculated by multiplying the RW by the EAD.
- PD: probability of default.

I calculated and compared two approaches:
- Standard approach. I used the whole [loan standardized approach (section 20.82)](https://www.bis.org/basel_framework/chapter/CRE/20.htm) to calculate the main metrics: LTV, EAD, RW, RWA. 
- F-IRB approach (Foundation-Internal Ratings Based), which is a method used by banks to calculate the amount of capital they need to hold for credit risk under the Basel III framework. The F-IRB approach allows banks to use their own internal models to estimate risk parameters such as probability of default (PD), loss given default (LGD), and exposure at default (EAD). For this approach, I created a Logistic regression model. 

## My results:
- The **probability of default** (PD) for the borrower is **38.7%**. 

In other words, out of 100 borrowers with similar characteristics to the borrower in this dataset, we would expect 38 of them to default on their loan. This value can be used as an input in calculating other risk metrics such as Expected Loss or Unexpected Loss.

**The first approach:**

The first approach uses a standard approach to calculate capital requirements based on the risk weight (RW) and the total EAD (exposure at default).
- Total EAD: 326 180 696.63
- Total RWA: 107 574 769.94
- RW: 32.98 %
- Capital requirement: 8 605 981.59

**The second approach F-IRB:**

The second approach uses the F-IRB (foundation internal ratings-based) approach, which allows banks to use their own internal models to estimate credit risk parameters such as PD, LGD (loss given default), and EAD.
- Total EAD: 326 180 696.63
- Total RWA_2: 707 442 092.23
- RW_2: 216.89 %
- Capital requirement_2: 56 595 367.38

In this case, we can see that the second approach leads to a significantly higher RWA (risk-weighted assets) and capital requirement than the first approach, which may indicate that the bank's internal model is more conservative than the standard approach.

**Logistic Regression metrics:**
- The **confusion matrix** shows that the model correctly classified 0 as 0 in **83%** of cases and 1 as 1 in **74%** of cases. 
- The overall **accuracy** of the model is 0.81, meaning that it correctly classified **81.16%** of the instances. But this dataset has imbalance data (BAD). 

- The **precision** of the model is 0.51, which means that out of all the instances that the model predicted as positive (1), only **51.1%** were actually positive. This suggests that the model may be too soft in predicting positive instances, which may result in a higher false positive rate.
- The **recall** of the model is 0.78, which means that out of all the actual positive instances, the model correctly identified **77.99%** of them. This indicates that the model has a good ability to detect positive instances, but there may still be some positive instances that the model missed.

- The **F1 score** is a measure of the model's accuracy that considers both precision and recall. It is calculated as the harmonic mean of precision and recall, and its value in this case is **61.74%**. A higher F1 score indicates better performance of the model in predicting both positive and negative instances.
