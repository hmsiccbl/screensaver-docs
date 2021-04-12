---
layout: default
title: Administration 
nav_order: 4
has_children: true
---

# Screensaver administration
{: .no_toc }

1. TOC
{:toc}
---

## User Management

Use the "Add user" button on the bottom of the left panel to add a new user account to the system.

### User  Account type

A User account (record) may be marked as a "Staff"; otherwise the user record is a "Screener" account.
* **Staff** accounts may be assigned read and write permissions on resources and fields.
  * Permissions are managed by assigning users to groups and permissions to the group.
* **Screener** accounts are for the individuals who will use the screening facility to conduct experiments.
  * Permissions are managed by the data sharing rules that have been implemented for the facility.

### User classification

The user classification identifies the role of the Screener in the experiments:
* **Principal Investigator** classification is reserved for user accounts that will be designated as the Principal Investigator for Screens (experiments).
  * Principal Investigator accounts may have lab members assigned.
* Other **non-staff classifications** identify non-PI screener accounts.
  * non-PI screener accounts must be assigned as a "lab member" to a PI user account.
* **Staff classifications** are reserved for administrative user accounts.

### Assign a username

In order to be able to log in, the new user account must be assigned a User ID.
* ICCB-L specific accounts should be assigned an **Ecommons ID** - this will server as the username.
* Other accounts should be assigned a **Username**.
  * Note: Screensaver does not provide an interface for direct management of user passwords. The ICCB-L Authorization system (TODO: link) provides a mechanism to proxy the user login action to the Harvard Ecommons system.
  * The [Django Admin Interface](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/) may be used by administrative accounts to set user passwords.

### Set the user data sharing level

For screener accounts created on systems using the ICCB-L authorization implementations, a data sharing level must be assigned to these accounts after creation in order for the account to be "active" (allowing log in).

## Library Management

* A **library** defines the plate formats and identities of the reagents of a collection,
* a **library copy** tracks the physical plates created with reagent stock.

A **library plate** is a grid of **wells** containing reagents. Plates are assigned a **plate number**; and the plates of a library are assigned consecutive numbers. Each well in the plate is assigned a **well ID**. The well ID is composed of the plate number represented with 5 digits and the **well name**. The well name encodes the location of the well on the plate; the row is encoded as a character, begining with "A" for the first row, and the column is encoded as a two digit number, beginning with "01" for the first column. Therefore, the well ID of the first well of plate "1000" is `01000:A01`. In practice, leading zeros may be omitted, so an equivalent well ID is `1000:A01`; however for some uses, the 5 digit plate number is required (see [small molecule structure images](#small-molecule-structure-images) below).

A **library copy** is a physical set of plates created with the reagents of a library. 

In a high throughput screening facility, it is useful to have multiple copies of a library for different purposes. 
* a "master stock plates" copy may be created at a higher concentration and used to generate other copies,
* one or more "library screening" copies may be created for use in generating assay plates for primary screening,
* "cherry pick screening" copies may be created for use in generating custom plates for follow up screening.
In this way, the facility can minimize loss from freeze/thaw cycles when plates are removed from storage for screening; and also, screening plates may be repurposed as cherry pick plates to maximize usage and depletion of specific reagents.

### Create a new library

To create a new library, use the "Add library" button on the bottom of the left panel. When creating a new library, define the plate type, and the number of plates that will be used in the library. On creation, the system initialize each well of the created plates with the "undefined" placeholder. After the library has been created, well definitions can be uploaded.

&&&&&To create a new library, use the "Add library" button on the bottom of the left panel. When creating the library, select from the defined drop-down lists for "Screen Type", "Plate Size", "Solvent", and "Screening Status". "Short Name" and "Library Name" accept free-form text values and must be unique, with the short name library value displayed by default when vieiwng the list of libraries. Both cannot be edited from the UI after library creation. "Provider" is the name of the vendor or other source. Since this is not a defined value, if used in other libraries an attempt should be made to match the name with previous entries. 

Select "Pool" if wells contain more than one reagent.

"Start Plate" and "End Plate" must be unique values and should reflect the expected number of plates in the library. If only one plate then both start and end plate should be entered as the same value. Once set, start and end plate cannot be edited from within the UI.

"Description" is not a required field and accepts any desired text that provides additional information about the library.

After selecting "Save", optional admin comments can be added. These are visible only to users with admin privileges.

On creation, the system initializes each well of the created plates with the "undefined" placeholder. After the library has been created, well definitions can be uploaded.&&&&&

### Upload library well definitions

To upload library well definitions, use the "Upload" button on the library details tab.

See [Library File Formats](library-file-formats.html)

### Create a library copy

To create a library copy, go to the "Copies" tab of a library and use the "Add" button.

* A copy should have a short unique name assigned to it.
* Assign an initial plate well volume: this is the initial volume of reagent in all well of the plates for the copy.

### Small molecule structure images

Structure images may be associated with each of the wells of the library.
* Image files should be stored in a directory specified by the `WELL_STRUCTURE_IMAGE_DIR` in the [settings.py](setup-configuration.html#create-a-limssettingspy) file. This path must be visible to all instances of the Screensaver server.
* Generating images
  * Use third-party rendering software such as [The Chemistry Development Kit](https://cdk.github.io/) to generate images for each small molecule. 
  * Image files must be named using the `<5-digit plate number>` follwed by the`<well_name>`.
    * For example, a PNG image for the small molecule in Plate `1005`, Well `G15` would be named `01005G15.png`. 
* Place the image files in a file system directory structure, partitioning the image files into subdirectories named by plate number (5 digits, left-padded with zeros). 

## Screen and Study Management

A screen tracks the progress of performing a screening assay, including a description of its biological significance, its experimental protocol, and additional data to support the administrative needs of the facility. After screening data is generated, this data may uploaded and associated with the screen record.

A study is similar to a screen, except that the reagents and the data associated with the study are based on publications or other research data and not on a screening assay performed at the facility. 

### Create a new screen

To create a screen, use the "Add screen" button on the bottom of the left panel.

### Record a library screening visit

When screens are conducted at the facility, the plates of one or more library copies are used to produce the assay plates used for screening. The usage of library copy plates is tracked in Screensaver by adding new "Library Screening" activities. Each library screening activity tracks the set of library copy plates that have been used, along with the volume of reagent that was taken from each library copy well and the number of assay plate replicates that were produced. In this way, the Screensaver database can be used calculate the number of times each copy has been used as well as the total consumed and remaining reagent volume of every library copy plate. 

To add a new library screening visit, go to the "Activities" tab of the Screen, and use the "Add library screening visit" button.

see [Library screening visit](library-screening.html)

### Recording service activities

**Service Activities** record the different tasks that staff will perform when administering a HTS screening assay. 

To add a new service activity, go to the "Activities" tab of the Screen, and use the "Add library service activity" button.

### Upload screen results

After the screening assay has been performed, the results of this assay may be formatted and uploaded to the Screensaver database.

See [Screen Result File Format](screenresult-file-format.html)

&&&&&Screen results are loaded from the "Data" view within a screen. The Excel file for result loading has 3 worksheets:

"screen": indicates the facility_id (screen #)

"data_column": The worksheet where data columns are defined. Column name, title, data type, decimal places (for non-integer numeric), read-out type (for raw data), and how derived (for result values calculated from raw data) are defined here. "Name" is a shortened, lower case version of the title, and used for defining columns used for derived values. "Title" indicates the column headers that will be displayed in the data view for a screen. 

Screen positives are defined as either boolean_positive_indicator (with positive = TRUE) or partition_positive_indicator (with positive either S, M, or W). These are the wells that are counted for total positives in the positives summary.

"data": All screen result data values are included here. The first two columns (plate_number, well_name) must be specified for every result record. Records with duplicate plate_number / well_name will result in a loading failure and must be corrected. The assay_control_well_type column should only values for wells that are assay controls (N, P, or O). Specific well columns can be excluded based on screener input from the annotated result file in the "exclude" column by using the "name" headers defined in the data column worksheet. 

Subsequent columns are for result data defined in the data columns worksheet. Columns that are not defined will not display after loading. Note that data columns must use the "name" header.

After the initial data loading, data column definitions can be viewed within the "Data Columns" tab in the data view. Details on loading failures can be viewed by clidking on Job: #.&&&&&

### Raw data transformation

Screening assay result data are detected by different **plate reader** devices. These devices may produce the **raw data** results in different formats including text or CSV.

The **Raw Data Transformer** utility in Screensaver may be used to parse these raw data results, and to collate read-out types, replicates and conditions that are measured, and to associate these collated results with plate and well data from the screensaver database. The Raw Data Transformer output can then be entered into the [Screen Result File Format](screenresult-file-format.html).

see [Raw Data Transformer](raw-data-transformer.html)

### Recording "cherry pick" or "follow-up" reagent requests 

When anaylizing the screen results for an experimental assay, specific reagents may be identified as significant and selected for follow-up assays. "Cherry picking" is term used for this selection process.

To create a "cherry pick request", select the "Cherry picks" tab on the screen page, and then use the "add" button.

For details on the cherry pick request process, see [Cherry Pick Request](cherry-pick-request.html)

### Create a study (in-silco screen)

A **Study** is similar to a **Screen** in that it is used to associate data with reagents in the Screensaver libraries. Therefore, the study data are formatted in an identical manner to the Screen result data and are uploaded in the same way.

See [Screen Result File Format](screenresult-file-format.html) for more details on this process.

&&&&&The "Add study" button is located at the bottom of the left menu panel. In "Study Details", "Library Screen Type", "Lab Name", and "Study Type" have defined values for selection. The "Study ID" should be created by adding 1 to the existing study with the highest number (not including reagent count and confirmed positives studies). "Title" and "Summary" are free text, required fields.Title, Lab Name, and Summary can be edited after study creation.

Following creation of a study, data can be uploaded using an Excel (.xlsx) in the same format as loading screen results. This is done using the "Load data" button in the Data section. Required fields are "plate_number" and "well_name". One or more data columns are then defined that will display the study data.&&&&&


## Search Utilities

The left hand panel shows different search entry boxes that may be used to locate plated reagents, aliquoted compounds (tubes), library copy plates, and cherry pick requests.

see [Search Utiilties](search-utilities.html) for more information.
