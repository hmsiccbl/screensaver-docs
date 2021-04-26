---
layout: default
title: Raw Data Transformer
nav_order: 13
parent: Screen Management
grand_parent: Administration
---
{: .no_toc }

1. TOC
{:toc}
---

# Raw Data Transformer

Screening assay result data are detected by different **plate reader** devices. These devices produce **raw data** results in different formats including text or CSV.

The **Raw Data Transformer** utility in Screensaver provides  these functions:
* parsing of the raw data output by the plate reader devices as matrices in text or csv format,
* collation of the multiple **library plates**, **read-out types**, **replicates**, and **conditions** represented,
* association of the raw data results with plate and well information from Screensaver.

The data from the **Raw Data Transformer** may then be entered into the [Screen Result File Format](screenresult-file-format.html) and uploaded to Screensaver.


# Transforming raw screening data

The Transform Raw Data Tab exists for each Screen on the Screening summary Tab.

## Input fields
The following fields are used to transform a raw data file into an ICCB-L formatted file:

* **Plate Ranges** - these are the library plate ids. They can be named one at a time (1701, 1702, 1703, etc) or in a range of ascending or descending plates (ie 1701-1703 or 1703-1701). The range also accommodate multiple ranges of plates separated by commas in the order you specify for example 2089-2090, 1701, 3260-3263, 1702
* **Output Filename** - automatically generated based on the Screen ID and the plate range. Format: “ScreenID_Plate Ranges” 
* **Output Format** - Choice of one library plate in one worksheet within the same workbook or all the plates combined into one worksheet.
* **Assay Plate Size** - Choice of 1, 96, 384, 1536 well plates
* **Assay Positive, Negative, Other Controls** - Adds the designation “P”, “N”, or “O” in the Type column of the ICCB-L formatted file to wells the user indicates. 
  * These wells can be written in manually A24, B24, etc in ranges A24-H24, or by column 23. A label can also be specified using the Well= “Label” format.
  * User can also use the Select Tab to choose wells by clicking on the wells in a plate format. Click the + on the left side, enter a label if desired, then manually click on the wells, click OK. The controls designation box is filled in for you. 
  * Labels appear for each well under the Pre-Loaded controls column in the ICCB-L formatted file.  
* **Library Plate size** - Plate as defined in Screensaver 1, 96, 384, 1536
* **Library Controls** - TODO: define this function
* **Comments** - For record keeping only - will not affect the ouput

## Input Files

Many configurations exist to accommodate the variety of raw data files that are provided to us.

You can specify a Readout Type, Conditions, Replicates and Readout names. The collation order determines the order the data is in the file and fills the data into the right column/plate based on the conditions, replicates, readout names. 

## Collation order examples

### Example#1: One Raw data File to one set of plates. 
* File - Browse to find the raw data file and attach here
* Collation - Plates-(Quadrants)-Conditions-Replicates-Readouts
* Readout Type - Absorbance
* Condition - blank
* Replicates - 2
* Readout names - Blank

For plates 1765-1770 the file will be filled In the following order based on the above requirements: 

1765 Rep A, 1765 Rep B, 1766 Rep A, 1766 Rep B, 1767 Rep A, 1767 Rep B, 1768 Rep A, 1768 Rep B, 1769 Rep A, 1769 Rep B, 1770 Rep A, 1770 Rep B

### Example #2: One Raw data File to one set of plates. 

* File - Browse to find the raw data file and attach here
* Collation - Replicates -Plates-(Quadrants)-Conditions-Readouts
* Readout Type - Absorbance
* Condition - blank
* Replicates - 2
* Readout names - Blank

For plates 1765-1770 the file will be filled in the following order based on the above requirements: 

1765 Rep A, 1766 Rep A, 1767 Rep A, 1768 Rep A, 1769 Rep A, 1770 Rep A, 1765 Rep B, 1766 Rep B, 1767 Rep B, 1768 Rep B, 1769 Rep, B1770 Rep B

### Example #3: Two Raw data File to one set of plates. 

* File1 - Browse to find the raw data file and attach here
* Collation - Plates-(Quadrants)-Conditions-Replicates-Readouts
* Readout Type - Absorbance
* Condition - blank
* Replicates - 2
* Readout names - Blank

(Click: "Add Input file")

* File2 - Browse to find the raw data file and attach here
* Collation - Plates-(Quadrants)-Conditions-Replicates-Readouts
* Readout Type - Luminescence
* Condition - blank
* Replicates - 2
* Readout names - Blank

For plates 1765-1770 the file will be filled in the following order based on the above requirements: 

1765 Rep A, 1765 Rep B, 1766 Rep A, 1766 Rep B, 1767 Rep A, 1767 Rep B, 1768 Rep A, 1768 Rep B, 1769 Rep A, 1769 Rep B, 1770 Rep A, 1770 Rep B for the absorbance data then 1765A-1771B for the luminescence Data

### Example #4 One Raw data File to one set of plates 2 replicates 2 timepoints 

* File - Browse to find the raw data file and attach here
* Collation - Plates-(Quadrants)-Conditions-Replicates-Readouts
* Readout Type - Absorbance
* Condition - blank
* Replicates - 2
* Readout names - T0, T60

For plates 1765-1770 the file will be filled In the following order based on the above requirements: 

1765 T0 Rep A, 1765 T60, RepA, 1765 T0 Rep B, 1765 T60 RepB ,1766 T0 Rep A, 1766 T60 RepA, 1766 T0 Rep B, 1766 T60 RepB, 1767 T0 Rep A, 1767 T60 RepA, 1767 T0 Rep B, 1767 T60 RepB

**Alternate collation:** If we chose Collation-Replicates -Plates-(Quadrants)-Conditions-Readouts

For plates 1765-1770 the file will be filled In the following order based on the above requirements: 

1765 T0 Rep A, 1765 T60 RepA, 1766 T0 Rep A, 1766 T60 RepA, 1767 T0 Rep A, 1767 T60 RepA, 1765 T0 Rep B, 1765 T60 RepB, 1766 T0 Rep B, 1766 T60 RepB, 1767 T0 Rep B, 1767 T60 RepB
