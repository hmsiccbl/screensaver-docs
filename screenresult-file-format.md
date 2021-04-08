---
layout: default
title: Screen Result File Format
nav_order: 5
parent: Administration
---

# Screen Result File Format



There are two types of sheets in a screen result data file:

   * =Data Columns= worksheet: Defines the data columns comprising the screen result.  It must be named "Data Columns" and must occur before the data worksheets.
   * =Data- worksheets:  Contains the actual screen result data values, across one or more worksheets.  The data worksheets include all subsequent worksheets and may have any name.  There is no restriction on the ordering or partitioning of screen result data across the worksheets (e.g. you may use a worksheet-per-plate partitioning, or place all data on a single worksheet if it fits).
   
---+++ =Data Columns= worksheet

A data column represents a series of values that are generated in the same
manner for each well in a screen result.  A data column may represent a series
of values returned from a plate reader, or a value that is calculated
(derived) from the values of other data columns.  If a screening has multiple
plate reader readout types (e.g. flouresence, luminescence, etc.), and/or
multiple replicates, and/or plate reads made at multiple time points, then
each combination will be represented by its own data column.

The =Data Columns= worksheet must contain the following labels in column A,
starting at row 1.  Data columns are defined one per column, starting at
column B.  Screensaver does not impose a strict limit on the number of data
columns.

| *Data Column Property* | *Required/Optional* | *Description* | *Value* |
| "Data" Worksheet Column | Required | The worksheet column that will contain the data values for this data column on each subsequent =Data= worksheet.  | Must be >= =E=.  In general, each subsequent data column will be in a subsequent column (=E=, =F=, =G=, etc.), although it is legal to skip columns. |
| Name | Required | A descriptive name for the data column  | Text |
| Data Type | Optional | The type of data contained in this column.  The =Positives Indicator= types specify that the values of this data column can be used to determine if the well was considered a "positive" result for the screen.  Multiple data columns can be declared as positive indicators (allowing the screen result to provide more than one interpretation of positives) | =Numeric= (default), =Text=, =Partition Positives Indicator=, =Boolean Positives Indicator=, =Confirmed Positive Indicator= |
| Decimal Places | Optional | If data type is =Numeric=, then this determines how many decimal places are to be shown when displaying the data for this data column; if left empty, the full precision of the data values will be displayed. | Non-negative number |
| Description | Optional | A full description of the data represented by this data column | Text |
| Replicate Number | Optional | The replicate number | Numeric |
| Time point | Optional | The time point at which the plate reader generated the data values. | Text. Screensaver handles this field as text, so any time format may be used.  However, a =HH:MM:SS= elapsed time format is recommended. |
| Time point ordinal | Optional | Used to assign an explicit ordering to the time points.  May be used in place of, or in addition to, "Time point"  | Number |
| Channel | Optional | For high content imaging, multiple channels may be used to take readings at separate wavelengths | Number |
| Zdepth ordinal | Optional | For high content imaging, defines the horizontal slice from which the image is taken | Number |
| Assay readout type | Optional | The readout technology used by the plate reader to generate the data values. | =Fluorescence Activated Cell Sorting=, =Fluorescence Intensity=, =FP=, =FRET=, =Imaging=, =Luminescence=, =Photometry=, =Unspecified= |
| If derived, how? | Optional | If Data Type derived, describes the calculation performed to produce the value | Text |
| If derived, from which columns? | Optional | If derived, the data columns that are used in the above calculation | A comma-delimited list of the ="Data" Worksheet Column= values for the data columns used in the calculation.  The specified data columns must be defined before (to the left of) the current data column. For legacy screen results, where only derived data columns exist (e.g. only a single "Positive" data column exists), the value may be =N/A=. |
| Primary or Follow Up? | Optional | Whether the data column contains data that was produced during the primary screening or a follow-up screening | =Primary= (default), =Follow Up= |
| Comments | Optional | Any additional comments | Text |


---+++ Data worksheets

Each data worksheet has 4 mandatory columns:

| *Column* | *Column label* | *Description* | *Value* |
| A | Plate | The plate number | =#####= |
| B | Well | The well name (row & plate) on a 384 well plate | =[A-P]##= e.g., L07 |
| C | Control Type | If the library well is empty and the assay plate well has been used as a control, define the assay well control type | =P= (Assay Positive Control(), =N= (Assay Control), =S= (Assay Control Shared, i.e., between screens) |
| D | Exclude | Optional. The column names of each data column value, for this well, that should be excluded.  An excluded value is one that is considered unusable for the purpose of determining positives | Optional.  =All=, or a comma-separated list of column names, if only some of the data column values for the well are unusable. |

Subsequent columns must contain the data for the data columns defined in the
=Data Columns= worksheet, matching the column placement specified by the
="Data" Worksheet Column=.

By convention, on the data worksheet, the first row of each data column column
will contain the name of the data column, but this is optional (and ignored by
the importer).

The acceptable values of each data column column are determined by the data column definition, as follows:

   * If data column's data type is a =Numeric=, then value must be a number
   * If data column's data type is a =Text=, then value must be text
   * If data column's data type is a =Partition Positive Indicator=, then value must be one of =S= (Strong), =M= (Medium), =W= (Weak)   
   * If data column's data type is a =Boolean Positive Indicator=, then value must be one of =Yes=, =No=, =True=, =False=, =0=, =1=
   * If data column's data type is a =Confirmed Positive Indicator=, then value must be one of =N=, =I=, =FP=, =CP= ("Not Tested", "Inconclusive", "False Positive", "Confirmed Positive")
