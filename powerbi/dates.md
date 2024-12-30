# working with dates

https://docs.microsoft.com/en-us/dax/format-function-dax

E.g.
* weekday: FORMAT(<date>, <"dddd">) -> Friday
* time: FORMAT(<date>, <"h:nn:ss">) -> "12:52:00"

Need date table with no gaps to leverage time intelligence

## create a date table

CALENDAR(<start_date>, <end_date>)

* returns a table with single column 'date' that contains a continuous set of dates *inclusive* of the specified dates

CALENDARAUTO(<fiscal_year_end_month>)

* returns a table with single column 'date' that automatically takes the earliest and latest date in model and internaly calls CALENDAR()

### dates table

> Modeling tab > New Table > CALENDARAUTO(12) 
> Model
> Date from Date table to Fact table
> Add column - New column
> Year = YEAR(Dates[Date])
> Day = DAY(Dates[Date])
> DayShortName = 
> Quick Measures: 
    * Rolling Average (for example)
    * Base value - what is being measured, e.g. price at close, average score, etc.
    * Adjust Period details - e.g. measuring every month, every week, every 3 years

> Line and Stacked Chart to visualise difference between Average and Rolling Average
* Date in Shared Axis
* Value in column values (from table)
* Rolling average (from measures) as line



