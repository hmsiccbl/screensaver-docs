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


# Libraries

## Terms

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

A **library copy** is a physical set of plates created with the reagents of a library. These physical plates of the library copy are known as **copy plates**.  

In a high throughput screening facility, it is useful to have multiple copies of a library for different purposes. 
* a "master stock plate" copy will have higher volumes and may be created at a higher concentration. These copy plates can then be used to generate other types of copy plates at lower concentrations and different volumes.
* "library screening" copies may be created for use in generating assay plates for primary screening,
* "cherry pick screening" copies may be created for use in generating custom plates for follow up screening.
In this way, the facility can minimize loss from freeze/thaw cycles when plates are removed from storage by only removing those plates designated for the defined purpose; furthermore, screening plates may be repurposed as cherry pick plates to replace differentially depleted plates.

## Creating a new library

To create a new library, use the "Add library" button on the bottom of the left panel. 
* "Short Name" and "Library Name" accept free-form text values and must be unique
  * The short name library value is displayed by default when vieiwng the list of libraries
  * Both cannot be edited from the UI after library creation.
* Select from the defined drop-down lists for "Screen Type", "Plate Size", "Solvent", and "Screening Status"
* "Provider" is the name of the vendor or other source. 
  * Since this is not a defined value, if used in other libraries an attempt should be made to match the name with previous entries.
* Select "Pool" if wells contain more than one reagent.
* "Start Plate" and "End Plate" must be unique values and should reflect the expected number of plates in the library. If only one plate then both start and end plate should be entered as the same value. Once set, start and end plate cannot be edited from within the UI.
* "Description" is not a required field and accepts any desired text that provides additional information about the library.
* After selecting "Save", optional admin comments can be added that will be stored with the revision log for the library. These comments will be visible only to users with admin privileges.

## Uploading library well definitions
* The system initializes all of the library well records with the "undefined" placeholder
* After the library has been created, well definitions can be uploaded for these "undefined" records.

Use the "Upload" button on the library details tab to show the **Upload dialog**.

Upload dialog:
* The upload format can be as an SD file if small molecule structure information (mol file) is to be included; otherwise content can be uploaded using an Excel file (.xlsx). 
* Comments can be added during the upload to include information regarding the loading session. 
* Set undefined library wells to "empty". If not selected all wells that have not been defined will remain in that state. If checked, all wells in the library that are not defined in the upload file will be set as empty. 
  * Note that well type may not be changed from the administrative interface after the initial loading, so only use this option if certain that the unspecified well types will not need to be changed from "empty". 

Uploaded well definitions must include:
* plate_number, 
* well_name, 
* library_well_type (experimental, dmso, empty, library_control), 
* either molar_concentration (where 0.01 = 10mM) or mg_ml_concentration. 
  * Concentration values are only permitted for wells with library_well_type = "experimental".
* see [Library File Formats](library-file-formats.html) for more information.

## Modifying library well defnitions

The field schema defines what fields may be updated after creation for the library well records.
* To access the schema, select the **Show field schema** option in the **Edit actions** menu on the library details page.

To modify data for existing records, first download the existing data using the **data interchange** mode:
1. Select "Add columns" in the well view and add the desired columns to include. 
2. Download a file (using "Download for data interchange"); this will output the correct column headers for data upload (if not known). 
3. Data can then be uploaded from the library details view as described above. 

Notes:
* For existing records, plate_number and well_name (or just well_id) are necessary to link the data to the appropriate wells. 
* Note that for any fields left blank in the loading file, the result will be that null values will be recorded in the corresponding well records. 
* Any empty columns that are not being used in the loading file should thus be removed, unless the intent is to remove values in that column for all wells in the loading file.
* The server will ignore unchanged values, however, if an entire column is unchanged, it is recommended to remove this column from the upload file to improve performance of the upload.

See the [Data Interchange](../reference/data-interchange.html) reference page for more information.

## Creating a library copy

To create a library copy, go to the "Copies" tab of a library and use the "Add" button.

* A copy should have a short unique name assigned to it. 
  * Names may contain spaces, underscores, numbers, and the letters [a-zA-Z].
  * A good practice is to name copies in increasing alphabetical order so that they will be sorted in  the order in which they will be used (in other words, copy "A" would be used before copy "B").
* Assign an initial plate well volume: this is the initial volume of reagent in all well of the plates for the copy.

## Small molecule structure images

Structure images may be associated with each of the wells of the library.
* Image files should be stored in a directory specified by the `WELL_STRUCTURE_IMAGE_DIR` in the [settings.py](setup-configuration.html#create-a-limssettingspy) file. This path must be visible to all instances of the Screensaver server.
* Generating images
  * Use third-party rendering software such as [The Chemistry Development Kit](https://cdk.github.io/) to generate images for each small molecule. 
  * Image files must be named using the `<5-digit plate number>` follwed by the`<well_name>`.
    * For example, a PNG image for the small molecule in Plate `1005`, Well `G15` would be named `01005G15.png`. 
* Place the image files in a file system directory structure, partitioning the image files into subdirectories named by plate number (5 digits, left-padded with zeros). 

# Aliquotted compound collections

The aliquotted compound collections are collections of reagents that are stored in single unit containers (tubes). 
* Each aliquotted compound record is defined by a **Facility ID**. 
* Each aliquot unit (tube) is defined by a unique **barcode** and is assigned to a aliquotted compound record.
* The collections are divided by the **collection name** 
  * For instance, the ICCB-L collection names are: **ICCBL**, **LSP**, **Ludwig**, and **MassCPR**

Note: the term "aliquot" and "tube" are equivalent.

## Browsing

* **Compounds** - go to the **Libraries** menu, then double click on the **Aliquoted Compounds** link.
* **Aliquots** (tubes) - go to the **Libraries** menu, then single click on the **Aliquoted Compounds** link. Each of the submenus will link to a listing of aliquots by **collection name**

## Creating new compounds

* Use the **Download blank template for upload** button to generate a template file with all updateable fields.
* After filling out the template file, use the **Upload compound data** button to load the new compounds to the system.
  * See the [Data Interchange](../reference/data-interchange.html) reference page for more information.
* To enter just one new compound at a time, click the **Add a compound** button. 

## Creating new aliquot units (tubes)

* Once the compound records have been created and assigned **Facility IDs**, new tube records can be assigned to these compounds.
* Screensaver requires that each tube record be assigned a unique **Barcode**.
  * Note that aliquot storage systems, such as the Arktic, generate these barcodes.

### Creating aliquots for a particular compound

* First navigate to the detail view for that compound
* Click the **"Add tubes"** button
  * New aliquot (tube) entries may be created by entering the **barcode** and the **volume** (in uL) on each line.

### Creating aliquots for many compounds at once

* Navigate the one of the tube collections
* Under the **edit actions** submenu
  * Use the **Generate template file for upload** button to generate a template file with all updateable fields.
  * After filling out the template file, use the **Upload tube data** button to load the new tube entries to the system.


See the [Data Interchange](../reference/data-interchange.html) reference page for more information.
