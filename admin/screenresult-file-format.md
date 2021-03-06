---
layout: default
title: Screen Result File Format
nav_order: 14
parent: Screen Management
grand_parent: Administration
---
{: .no_toc }

1. TOC
{:toc}
---

The Screensaver API supports the upload of experiment result data formatted in Excel workbooks. 

To load a screen result workbook, navigate to the screen, click the **Data** tab, then the **Screen Results** tab, and use the **Load data** option under the **Edit actions** menu.

After the initial data loading, data column definitions can be viewed within the "Data Columns" tab in the data view. Details on loading failures can be viewed by clidking on Job: #.

## Getting started with a template file

The Screensaver API will generate a "screen result template" file that is a valid screen result file that may be used as a template to create a new screen result file for upload.
* Mock data columns for each type of assay_data_type that can be recorded.
* Mock data for each of the mock columns.

## Screen Result File Format

The Excel file for result loading has 3 worksheets:
* "screen": indicates the facility_id (screen #)
* "data_column": The worksheet where data columns are defined. 
* "data": all sheets after the "data_column" sheet will be read in as data sheets.

## Data Columns worksheet

Each of the columns of data on the data worksheets are defined in the data columns worksheet.

A data column represents a series of values that are generated in the same
manner for each well in a screen result.  A data column may represent a series
of values returned from a plate reader, or a value that is calculated
(derived) from the values of other data columns.  If a screening has multiple
plate reader readout types (e.g. flouresence, luminescence, etc.), and/or
multiple replicates, and/or plate reads made at multiple time points, then
each combination will be represented by its own data column.

Data Column fields:

* **name** - the name of the column that will be used on the data worksheets: should contain only the letters a-z and the underscore "_" character. 
* **title** - the title for the data column that will be displayed in the Web application, may contain any character or spaces,
* **assay_data_type** - the type of the data being entered in this column, see [assay_data_type](#assay_data_type)
* **decimal_places** - (needed for decimal values only)
* **description** - a short description that will be shown in the Web application for the column,
* **comments** - more detailed description of the column that can be viewed on the data columns page in the application,
* **replicate_ordinal** - (optional) - the replicate number
* **time_point** - (optional) - a text representation of the time point at which the data for this column was read
* **assay_readout_type** - (optional) - the readout technology used to measure the data values for this column. See the generated [screen result template](#getting-started-with-a-template-file) for the set of recognized values.
* **how_derived** - (optional) - if applicable, a description of how the the data for this column are derived from data in other columns
* **derived_from_columns** - (optional) - a comma separated list of the column names from which the data for this column were derived
* **is_follow_up_data** - (default false) - whether the data column contains data that was produced during the primary screening or a follow-up screening
* **screen_facility_id** - (optional) - if a value other than the screen facility ID being loaded is entered, then this column is ignored
* **ordinal** - (optional) - if entered, this value overrides the order in which the columns are listed

### assay_data_type

The **assay_data_type** defines the type of data that are allowed in the data column on the data worksheets:
* **string** - any valid text may be entered 
* **integer** - integer values only
* **decimal** - any numerical value; to be represented with fixed precision (see **decimal_places**) 
* **boolean** - a binary measurement; ("true", "TRUE", or "1" represent a true value), 

Screen positives columns:

If the assay_data_type is a **positives indicator**, then "positive" values in this column mark the result as a positive hit, and are counted for total positives in the positives summary.

* **boolean_positive_indicator** - a true value indicates that the data point represents a positive determination,
* **partition_positive_indicator** - one of: "s" - (Strong), "m" - (Medium), "w" - (Weak), or "np" - (Not Positive); blank values are interpreted as not positive,
* **confirmed_positive_indicator** - one of: "cp" - (Confirmed positive), "fp" - (Positive determined from a false value), "i" - (Inconclusive), or "np" (Not positive); blank values are interpreted as not positive.

### assay_readout_type

The **assay_readout_type** defines the readout technology used to measure the data values for this column. See the generated [screen result template](#getting-started-with-a-template-file).

## Data worksheets

Any worksheet after the **data_column** worksheet will be read as a worksheet containing screen result data (*except for the special "reference" worksheet*).

Each data worksheet has 4 mandatory columns:

The first two columns (plate_number, well_name) must be specified for every result record. Records with duplicate plate_number / well_name will result in a loading failure and must be corrected. The assay_control_well_type column should only values for wells that are assay controls (N, P, or O). Specific well columns can be excluded based on screener input from the annotated result file in the "exclude" column by using the "name" headers defined in the data column worksheet.

Subsequent columns are for result data defined in the data columns worksheet. Columns that are not defined will not display after loading. Note that data columns must use the "name" header.

| *Column* | *Column label* | *Description* | *Value* |
|---|---|---|---|
| A | Plate | The plate number | =#####= |
| B | Well | The well name (row & plate) on a 384 well plate | =[A-P]##= e.g., "A07" |
| C | Control Type | If the library well is empty and the assay plate well has been used as a control, define the assay well control type | "p" (assay positive control), "n" (assay negative control), "o" (other) |
| D | Exclude | Optional. The column names of each data column value, for this well, that should be excluded.  An excluded value is one that is considered unusable for the purpose of determining positives | Optional.  "all", or a comma-separated list of column names, if only some of the data column values for the well are unusable. |

Subsequent columns must contain the data for the data columns defined in the **data_columns** worksheet, with the **name** of the data column used as the column header (row 1).

