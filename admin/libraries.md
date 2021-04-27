---
layout: default
title: Library Management
nav_order: 7
parent: Administration
has_children: true
---
{: .no_toc }

1. TOC
{:toc}
---

## Library Management Terms

* A **plated library** is a collection of reagents contained in library plates,
* A **library plate** is a grid of **wells** containing reagents: 
  * plates are assigned a **plate number**,
  * the plates of a library are always assigned consecutive plate numbers.
* A **well** is one location containing a reagent in a library plate, 
  * The **well name** encodes the location of the well on the plate; the row is encoded as a character, begining with "A" for the first row, and the column is encoded as a two digit number, beginning with "01" for the first column. 
  * The **plate number** and **well name** combine to form the **well ID** which may be used to identify any well and reagent in the library collection. 
  * Therefore, the well ID of the first well of plate "1000" is `01000:A01`. 
  * In practice, leading zeros may be omitted, so an equivalent well ID is `1000:A01`; however for some uses, the 5 digit plate number is required (see [small molecule structure images](#small-molecule-structure-images) below).

## Library copies

A **library copy** is a physical set of plates created with the reagents of a library. 

In a high throughput screening facility, it is useful to have multiple copies of a library for different purposes. 
* a "master stock plate" copy may be created at a higher concentration and used to generate other copies,
* "library screening" copies may be created for use in generating assay plates for primary screening,
* "cherry pick screening" copies may be created for use in generating custom plates for follow up screening.
In this way, the facility can minimize loss from freeze/thaw cycles when plates are removed from storage by only removing those plates designated for the defined purpose; furthermore, screening plates may be repurposed as cherry pick plates to replace differentially depleted plates.

## Creating a new library

To create a new library, use the "Add library" button on the bottom of the left panel. When creating the library, select from the defined drop-down lists for "Screen Type", "Plate Size", "Solvent", and "Screening Status". "Short Name" and "Library Name" accept free-form text values and must be unique, with the short name library value displayed by default when vieiwng the list of libraries. Both cannot be edited from the UI after library creation. "Provider" is the name of the vendor or other source. Since this is not a defined value, if used in other libraries an attempt should be made to match the name with previous entries.

Select "Pool" if wells contain more than one reagent.

"Start Plate" and "End Plate" must be unique values and should reflect the expected number of plates in the library. If only one plate then both start and end plate should be entered as the same value. Once set, start and end plate cannot be edited from within the UI.

"Description" is not a required field and accepts any desired text that provides additional information about the library.

After selecting "Save", optional admin comments can be added. These are visible only to users with admin privileges.

On creation, the system initializes each well of the created plates with the "undefined" placeholder. After the library has been created, well definitions can be uploaded.

## Upload library well definitions

To upload library well definitions and content information, use the "Upload" button on the library details tab.The upload format can be as an SD file if small molecule structure information (mol file) is to be included; otherwise content can be uploaded using an Excel file (.xlsx). Comments can be added during the upload to include information regarding the loading session. For all wells to be uploaded, required fields are plate_number, well_name, library_well_type (experimental, dmso, empty, library_control), and either molar_concentration (where 0.01 = 10mM) or mg_ml_concentration. Concentration values are only permitted for wells with library_well_type = "experimental".

After selecting the "Upload" button and setting the file to be used for upload, there is an option to set undefined library wells to "empty". If not selected all wells that have not been defined will remain in that state. If checked, all wells in the library that are not defined in the upload file will be set as empty. Attempts to load content for these wells will subsequently fail so only use this option if certain that the well type will not need to be changed. Updating of library well type is not possible using the UI or through data file upload.

To add data for new records or existing records, select "Add columns" in the well view and check the desired columns to include. Download a file (using "Download for data interchange") to determine the correct column headers (if not known). Data can then be uploaded from the library details view. For existing records, plate_number and well_name (or just well_id) are necessary to link the data to the appropriate wells. Note that for any fields left blank in the loading file, the result will be null values in the corresponding well records. Any columns that are not being used in the loading file should thus be removed, unless the intent is to remove values in that column for all wells in the loading file.

See [Library File Formats](library-file-formats.html) for more information..

## Create a library copy

To create a library copy, go to the "Copies" tab of a library and use the "Add" button.

* A copy should have a short unique name assigned to it.
* Assign an initial plate well volume: this is the initial volume of reagent in all well of the plates for the copy.

## Small molecule structure images

Structure images may be associated with each of the wells of the library.
* Image files should be stored in a directory specified by the `WELL_STRUCTURE_IMAGE_DIR` in the [settings.py](setup-configuration.html#create-a-limssettingspy) file. This path must be visible to all instances of the Screensaver server.
* Generating images
  * Use third-party rendering software such as [The Chemistry Development Kit](https://cdk.github.io/) to generate images for each small molecule. 
  * Image files must be named using the `<5-digit plate number>` follwed by the`<well_name>`.
    * For example, a PNG image for the small molecule in Plate `1005`, Well `G15` would be named `01005G15.png`. 
* Place the image files in a file system directory structure, partitioning the image files into subdirectories named by plate number (5 digits, left-padded with zeros). 

## Aliquotted compound collections

In addition to the plated library collections, Screensaver also manages aliquotted compound collections. These are reagents stored in individually managed aliquots (aka "tubes").




