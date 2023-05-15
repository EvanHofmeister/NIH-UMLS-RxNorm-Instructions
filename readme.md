## Instructions for setting up database from NIH UMLS RxNorm Files

![Pipeline](images/Pipeline.png)


First sign-up for a 'UMLS Terminology Services Account' so you can download files:
* [UMLS Sign-Up](https://uts.nlm.nih.gov/uts/signup-login)

Next download the latest RxNorm files:
* [RxNorm Files](https://www.nlm.nih.gov/research/umls/rxnorm/docs/rxnormfiles.html)



Below are the top 10 series available:
| None | indicator_id | indicator                                                                          | category            |
|------|--------------|------------------------------------------------------------------------------------|---------------------|
| 0    | ZSFH         | ZHVI Single-Family Homes Time Series ($)                                           | Home values         |
| 1    | ZCON         | ZHVI Condo/Co-op Time Series ($)                                                   | Home values         |
| 10   | SSSW         | Median Sale Price (Smooth, SFR only, Weekly View)                                  | Inventory and sales |
| 12   | SSAW         | Median Sale Price (Smooth, All Homes, Weekly View)                                 | Inventory and sales |
| 18   | SASW         | Median Sale Price (Smooth & Seasonally Adjusted, SFR only,   Weekly View)          | Inventory and sales |
| 20   | SAAW         | Median Sale Price (Smooth & Seasonally Adjusted, All   Homes, Weekly View)         | Inventory and sales |
| 22   | RSSA         | ZORI (Smoothed, Seasonally Adjusted): All Homes Plus   Multifamily Time Series ($) | Rentals             |
| 23   | RSNA         | ZORI (Smoothed): All Homes Plus Multifamily Time Series ($)                        | Rentals             |
| 24   | NSAW         | Median Days to Pending (Smooth, All Homes, Weekly View)                            | Inventory and sales |
| 28   | MSAW         | Mean Days to Pending (Smooth, All Homes, Weekly View)                              | Inventory and sales |


Additional instructions provided by NIH NLM below:
* [UMLS Homepage](https://www.nlm.nih.gov/research/umls/index.html)

* [Video tutorial for Querying RxNorm Tables](https://www.nlm.nih.gov/research/umls/user_education/quick_tours/RxNorm/ndc_rxcui/NDC_RXCUI_DrugName.html)

* [RxNorm technical documentation](https://www.nlm.nih.gov/research/umls/rxnorm/docs/techdoc.html#s13_0)





## Mapping NDC, RXCUI, and Drug Names in the RxNorm Files

``` sql
SELECT rs.atv as ndc, rs.rxcui, rc.str
FROM rxnsat rs, rxnconso rc
WHERE rs.atn = 'NDC'
AND rs.rxaui = rc.rxaui
AND rc.sab = 'RXNORM'
AND rc.tty in ('SCD','SBD','GPCK','BPCK')
ORDER BY rc.str;
```