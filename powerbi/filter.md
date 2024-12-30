## filter functions

* can evaluate an expression within one, two, or more filter contexts
* often used with intermediate functions such as ALL() which ignores any filters which might have been applied

ALL() - ignores any filters

Total Sales = SUM(Orders[Sales])
Total Sales ALL = CALCULATE([Total Sales], ALL(Orders))

FILTER(<table>, <filter>) - returns a filtered table

Total Sales Chuck = 
CALCULATE(
    [Total Sales], 
    FILTER(Fact_orders, 
        RELATED(Dim_Sales[SalesPerson]) = "Chuck")
)

RELATED() - returns values for related table

CROSSFILTER(<col1>, <col2>, <direction>) - specifies the cross-filtering direction between two columns
* can override relationship in data model

Benefits of filtering in DAX: 
* improves performance - filters out unnecessary data, defines specific relationships between tables
* reusability - refer to oterh calculated measures
* complex computations - concise syntax

Counting

COUNT(<column>) - rows with numbers, dates, strings in a column
COUNTA(<column>) - amount of rows with numbers, dates, strongs or booleans in a column
COUNTBLANKS(<column>) - number of blank rows
DISTINCTCOUNT(<column>) - number of distinct values in a column
COUNTROWS(<table>) - amount of rows with numbers, dates, and strings in a table

