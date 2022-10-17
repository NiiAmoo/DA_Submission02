
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Big Pharma Product Forecast

<!-- badges: start -->
<!-- badges: end -->

The goal of this project is to forecast product demand for Big Pharma, a
large pharmaceutical distribution company in Germany.

**The Business Problem**

Big Pharma restock their warehouses monthly, but often run into issues
with:

1.  Overstocking - having too much of a product available without
    corresponding consumer demand.
2.  Understocking - having too little products avaialbe to meet consumer
    demands.

**Tasks**

The goal is to offer Big Pharma a solution to their problem. The
proposed solution is a time series forecast of their product demand. we
begin with a pilot test to forecast the quantity of products the company
should purchase for their warehouses in the coming month.

**Data** Contains product demand data from October 2020 to July 2021
with the following fields:

1.  Date: The date a product was purchased
2.  Product ID: The ID for the product
3.  Stock Demand: The quantity of product purchased (unit is in boxes)

Below is a summary of the data.

    #>       date              product_id       stock_demand      
    #>  Min.   :2020-10-01   N0SI1  :   1482   Min.   :-12226.00  
    #>  1st Qu.:2020-12-10   AL10C  :   1269   1st Qu.:     3.00  
    #>  Median :2021-02-23   ET0N1  :   1259   Median :     9.00  
    #>  Mean   :2021-02-21   V0EL1  :   1250   Mean   :    79.71  
    #>  3rd Qu.:2021-05-04   1PO0L  :   1195   3rd Qu.:    31.00  
    #>  Max.   :2021-07-31   0TR2A  :   1188   Max.   :149004.00  
    #>                       (Other):1040932

### Analysis & Modeling

We have a demand value of `-12226`. However, since stock demand is the
number of boxes of the product that was purchased (according to our meta
data dictionary) then it should not be negative.

Turns out there are quite a number of records (`6,808`) with stock
demand below `0`. To handle this, we make the following assumptions.

**Assumption:**

-   Negative stock demand represents shortage. ie. Customers requested
    the said number of boxes of the product, but they were out of
    stock.  
-   Zero stock demand represents no demand for the product for that day.

In order to accurately forecast the shortages(negative `stock_demand`),
I converted them to positive values and model them as real demand
values. This will ensure stock in the warehouse meets customer demands.

Next, there are over 7000 unique products available for analysis and
forecasting. For this test case,

-   Products for this exercise are restricted to the top 30 products
    based on `stock_demand`.

This allowed me to focus on the most important products and quickly
iterate to generate a working solution.

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
![](README_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

You’ll still need to render `README.Rmd` regularly, to keep `README.md`
up-to-date. `devtools::build_readme()` is handy for this. You could also
use GitHub Actions to re-render `README.Rmd` every time you push. An
example workflow can be found here:
<https://github.com/r-lib/actions/tree/v1/examples>.

You can also embed plots, for example:

![](README_files/figure-gfm/pressure-1.png)<!-- -->

In that case, don’t forget to commit and push the resulting figure
files, so they display on GitHub.
