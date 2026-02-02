# Sales-Operations-Analytics
![Alt text](https://github.com/Ambogo2/Sales-Operations-Analytics/blob/main/dashboard-.png)

## Dataset
I used this [Dataset](https://github.com/Ambogo2/Sales-Operations-Analytics/blob/main/Dataset.xlsx) for my analysis and the data had 632 rows and 15 columns of transactional sales data

## Data Issues Found
|Column   | Issue Found| Notes |
|------------|------------|------------|
| Duplicates | There was 1 duplicate   | Removed the duplicate based on OrderID  |
| DiscountPct   | Values >30%   | Capped at 30%   |
| Incorect Data types|Most of the columns were not formatted correctly| Fixed the data types|
| City, Salesperson, and Channel  | Missing Values| Filled using the most common city for that Country, Replaced with “Unknown” when missing for sales person and Assigned based on majority channel used by that Salesperson; otherwise “Retail” as default   |
| UnitPrice|Negative values | Used find and replace tool to remove them |
| DiscountPct | Values >30% | Capped at 30% |
| RequiredDate | Some < OrderDate | Imputed as OrderDate + 3 days |

# Data  Cleaning Methodology
| Rule # | Column        | Cleaning Approach / Formula                              | Notes                              |
|------:|---------------|------------------------------------------------------------|------------------------------------|
| 1     | City          | =IF(TRIM(City)="","Unknown",City)                           | Handles missing text               |
| 2     | DiscountPct   | =IF(DiscountPct>0.3,0.3,DiscountPct)                        | Caps discounts to 30%              |
| 3     | LeadTimeDays  | =RequiredDate - OrderDate                                  | Derived field for service level proxy |
| 4     | GrossRevenue  | =UnitPrice * Quantity * (1 - DiscountPct)                  | Calculated field                   |
| 5     | PriceBand     | Quantile-based categorization                               | Low / Medium / High                |


## Data Enrichment
I Created calculated columns using the following formulas
- **GrossRevenue** = `UnitPrice × Quantity × (1 − DiscountPct)`
- **CostOfGoods** = `UnitCost × Quantity`
- **GrossProfit** = `GrossRevenue − CostOfGoods`
- **MarginPct** = `IF(GrossRevenue = 0, 0, GrossProfit / GrossRevenue)`
- **LeadTimeDays** = `RequiredDate − OrderDate`
- **Month** =`MMM-YYYY from OrderDate`
- **Quarter** =`Q#-Year`
- **PriceBand**=`SKU grouped into Low/Medium/High using revenue quantiles`

## Assumptions Made

- Discounts above 30% are likely data entry errors or policy violations
- Missing Salesperson does not invalidate the order
- Delivery lead time should not be negative
- PriceBand classification reflects relative pricing, not cost

## Dashboard Insights


