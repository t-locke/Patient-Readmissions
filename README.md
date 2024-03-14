# Patient-Readmissions
Study patient readmission within 60 days of discharge based on age, chronic conditions, and total costs. Using Machine Learning, I want to find out if we can predict when a patient will be readmitted after discharge so that we can better prepare to “take care” of them to minimize any chance from coming back to the hospital (readmission).
Data Preparation
I chose the provided dataset from CMS for analytics: 
DE1_0_2008_to_2010_Inpatient_Claims_Sample_13.csv
DE1_0_2008_Beneficiary_Summary_File_Sample_13.csv
Initially I was going to include all inpatients from 2008 thru 2010 for my study but as I started analyzing patient conditions (Column names with SP_*), I found that some chronic conditions appeared to one patient in 2008 but not in 2009 or 2010 of the same patient (matching DESYNPUF_ID). In order to have definitive chronic conditions for my study I decided to use beneficiary 2008 data only. See attached SQL code for how I extracted only inpatients that matched 2008 beneficiary.

I did some of the preliminary data analysis, extract and additions using SQL. These include:
-	A new inpatient table ‘Inpatient_Claims_2008_FUTURE_CHKIN’ with additional calculated columns:
-	 ‘FUTURE_CHECKIN’: Future check-in date (taken from the ‘next’ readmission date)
-	‘FUTURE_GAP’: Number of days between future readmissions
-	‘60_DAYS_READMIT’: Binary value either that patient readmitted within 60 days (1 or 0)
Modified the beneficiary table with the following additions:
-	‘BENE_AGE_ASOF_2008’: Patient’s age
-	‘BENE_AGE_CATS’: Age categories (‘AGE UNDER 55’, ‘AGE 55-64’, ‘AGE 65-74’, ‘AGE 75-84’, ‘AGE 85-94’)
-	All SP_* fields: Convert ‘1’ to ‘1’ and ‘2’ to ‘0’ (1=Yes, 0=No)
-	‘TOTAL_CONDITIONS’: Total number of chronic conditions of a patient
-	‘TOTAL_READMISSION’: Total number of readmissions of a patient
