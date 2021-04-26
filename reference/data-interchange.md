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

**Download for data interchange** insures that:
* **column headers** use the internal "name" of the column that does not contain spaces or special characters that may be used in the column "title",
* **raw numerical values** are exported instead of the values shown in the Web application which may have rounding rules or SI Unit conversion applied,
* **vocabulary keys** are exported instead of *vocabulary titles*.


