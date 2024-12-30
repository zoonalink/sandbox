https://learn.microsoft.com/en-us/dax/

## measures v calculated columns

* calculated columns on data import, visible in data and report panes
* measures calculated at query run-time, visible only in report pane

## context

* row, query, filter

### row 
* simplest - evaluates at row level, includes all values in the current row.  Calculated column is an example of row context
* query - subset of data returned by formula - slicers, page filters, table columns, row headers, interactions with visualisations
    * applied on top of row context
* filter - set of values allowed in each column or in values retrieved from related table; applied through argumetns in formular or report filters on row and column headings. 
    * applied last



RELATED()
* use to bring in columns from other tables - like a merge within powerbi


## best practices

* keep DAX measures grouped together - _measures or _calculated tables
* format and comment with DAX
    * indentations to increase understanding
    * // for comments
* use `variables` to improve formulas
    * stores result of expression as a named variable
    * can be used as an argument to other measure expressions
    * advantages: improve performance and readability, simplify debugging, reduce complexity
    * `VAR <name> = <expression>` followed by `RETURN` statement

Example: 

Sales growth = 

VAR
SALESPRIORYEAR = CALCULATE([SALES], SAMEPERIODLASTYEAR('DATE'))
RETURN

Sales growth = [SALES] - SALESPRIORYEAR



CROSSFILTER example: 

Count of chiller itesm = CALCULATE(
    COUNTROWS(FILTER(Dim_StockItem[Is Chiller Stock] = True)),
    CROSSFILTER(Dim_StockItem[Stock Item Key], Fact_Sales[Stock Item Key], Both)
)


## iterating functions

* operate on row-level to iterate over each row to perform some sort of expression
    * SUMX()
    * AVERAGEX()


* use filter function such as FILTER() to return a filtered table: 

SUMX(
    FILTER(
        <table>,
        <filter>,
        <expression>
    )
)

Total Costs East SUMX = 
SUMX(
    FILTER(
        Fact_orders,
        Fact_orders[Region] = "East"),
        Fact_orders[Sales] - Fact_Orders[Profit]
    )

RANKX() - ranks rows by a given expresssion

RANKX(
    <table>,
    <expression>
)

Example - rank regions by total costs: 

Total costs RANKX = 
RANKX(
    ALL(Dim_Sales[Region]),
    [Total Costs]
)

* ALL() means that the ranking happens without the filtering (query context) - otherwise they would all be 1


Example iterating function: 


Average Discount Rate = AVERAGEX(
    Fact_sales, 
    (Fact_sales[Retail Price] - Fact_sales[Unit Price]) / Fact_sales[Retail Price]
)


Discount Rate Ranking = RANKX(
    ALL(Dim_employee[Employee]), [Average Discount Rate]
)