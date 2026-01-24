# Sales-Operations-Analytics

## Dataset
I used this Dataset for my analysis and the data had 632 rows and 15 columns of transactional sales data

## Data Issues Found
|Column   | Issue Found| Notes |
|------------|------------|------------|
| Duplicates | There was 1 duplicate   | Removed the duplicate based on OrderID  |
| DiscountPct   | Values >30%   | Capped at 30%   |
| Incorect Data types|Most of the columns were not formatted correctly| Fixed the data types|
| City, Salesperson, and Channel  | Missing Values|    |
| UnitPrice|Negative values | Corrected to median of valid UnitPrices  |
| DiscountPct | Values >30% | Capped at 30% |
| RequiredDate | Some < OrderDate | Imputed as OrderDate + 3 days |

# Data Methodology
| Rule # | Column        | Cleaning Approach / Formula                              | Notes                              |
|------:|---------------|------------------------------------------------------------|------------------------------------|
| 1     | City          | =IF(TRIM(City)="","Unknown",City)                           | Handles missing text               |
| 2     | DiscountPct   | =IF(DiscountPct>0.3,0.3,DiscountPct)                        | Caps discounts to 30%              |
| 3     | LeadTimeDays  | =RequiredDate - OrderDate                                  | Derived field for service level proxy |
| 4     | GrossRevenue  | =UnitPrice * Quantity * (1 - DiscountPct)                  | Calculated field                   |
| 5     | PriceBand     | Quantile-based categorization                               | Low / Medium / High                |


