---
layout: default
title: Data Interchange
parent: Reference
nav_order: 5
---
{: .no_toc }

1. TOC
{:toc}
---

# Data Interchange

The Screensaver application uses the term **"Data Interchange"** to describe the process of retrieving data from the API, updating this data, and then loading the updated data back to the API.

The data in the Screensaver application are divided into "resources"; the **resource schema** defines the characteristics of the resource, and the **resource field schema** defines the characteristics of the fields of the resource. 

The **resource field schema** provides an accurate and up-to-date specification of the field **data_type**, **title**, **description**, as well as whether the field is required. If the field values are constrained by a **vocabulary**, this is also specified.


For more details on the resources and interaction with the API, see the [api-usage](../api-usage) section for more information. 

## Uploading data

Where data upload is integrated into the operation of the Web application, an **edit actions** sub-menu is provided:
* **Upload** - provides a dialog to choose the file of data to upload
* **Generate a template file** - will generate a template file containing all of the fields that may be modified for the resource, as well as reference information for field and vocabulary types.
* **Show the field schema** - will link to a query page showing the field schema (definitions of all of the fields) for the resource.

## Download data for data interchange 

When downloading data for modification and upload, the **Download for data interchange** option of the download dialog should be chosen to generate data.

To modify data for existing records, first download the existing data using the **data interchange** mode:
1. Select "Add columns" in the report view and add the desired columns to include. 
2. Download a file (using "Download for data interchange"); this will output the correct column headers for data upload (if not known). 
3. The data file can then be modified and uploaded back to the API. 

**Download for data interchange** insures that:
* **column headers** use the internal "name" of the column that does not contain spaces or special characters that may be used in the column "title",
* **raw numerical values** are exported instead of the values shown in the Web application which may have rounding rules or SI Unit symbols and conversion applied:
  * Volumes will be represented in raw liter values, so “30 uL” will be downloaded as “0.000030”
  * Concentrations will be represented in raw Molar values, so "10 mM" will be downloaded as "0.000010"
* **vocabulary keys** are exported instead of *vocabulary titles*.
  * Browse to **Admin** => **Vocabularies** to view the set of vocabularies for a particular field.

## Notes for uploading data
* Each reasource will have a key field (or set of fields); these are defined in the schema by the "id_attribute" and must be included in all uploaded records. 
* Fields that are left blank in the loading file will result in null values recorded in the corresponding records. 
* Any empty columns that are not being used in the loading file should thus be removed, unless the intent is to null out values in that column for all wells in the loading file.
* The server will ignore unchanged values, however, if an entire column is unchanged, it is recommended to remove this column from the upload file to improve performance of the upload.

