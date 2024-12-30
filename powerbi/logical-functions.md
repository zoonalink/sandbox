https://campus.datacamp.com/courses/intermediate-dax-in-power-bi/logical-functions?ex=1

IF(<logical_test>, <value_if_true>[, <value_if_false>])

AND(<logical1>, <logical2>) - TRUE if both TRUE
* &&

OR(<logical1>, <logical2>) - TRUE if at least one logical test is TRUE
* ||

NOT(<logical>) - changes the logical

SWITCH() - evaluates an expression against a list of values and returns one of multiple possible result expressions

* preferred over nested IF() functions

* SWITCH(<expression>, <value>, <result>[, <value>, <result>] ... [, <else>])



Measure

HASONEVALUE() - returns true if one value
* useful for blanking out results in totals

MeasureWOTotal = 
IF(
    HASONEVALUE<measure/column>, 
    RANKX(
        ALL(<measure/column>),
        <resultmeasure>
    ),
    BLANK()
    )

SWITCH example: 

Employee Performance Assistance =
SWITCH(
    TRUE,
    AND([Average Discount Rate] < 0.3296, [Profit Ratio] > 0.538), "HIGH",
    AND([Average Discount Rate] < 0.33, [Profit Ratio] > 0.537), "MEDIUM",
    "LOW"
)

CALCULATE SUM WHERE CONDITION MET, example

Calculated column to id type: 

* identify chiller item which are
* high volume (sales > 100) OR
* high price (retail price > 15)

High Price / Volume Chiller Item = 
    RELATED(Dim_StockItem[Is Chiller Item]) &&
    (Fact_Sales[Total Chiller Items] > 100 ||
    Fact_Sales[Retail Price] > 15)

THen use this in measure: 
* Calculate sum of sales for these items


Total Sales High Vol/Price Chiller = 
CALCULATE(SUM(Fact_Sales[Total Excluding Tax]),
Fact_Sales[High Price / Volume Chiller Item] = TRUE)