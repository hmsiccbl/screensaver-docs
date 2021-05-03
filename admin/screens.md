---
layout: default
title: Screen Management
nav_order: 8
parent: Administration
has_children: true
---
{: .no_toc }

1. TOC
{:toc}
---

# Screens

The **Screen** view is the central location for tracking the progress of a high throughput screening assay project. The different tabs of the Screen view show the details of the screening project, including a description of its biological significance, its experimental protocol, and additional data to support the administrative needs of the facility. 
* The **Screening summary** view keeps track of **Library screening visits** where the library plate copies screened, replicates created, volumes used, and facility resources required are tracked. 
* The **Data** view provides the interface to upload screening data, and also provides reporting capabilities that can be used to investigate the data and do cross-screen comparisons. 
* The **Cherry Picks** view keeps track of **Cherry Pick Request** follow up assays, providing query tools to locate library copies having the requested reagents and track volumes used a the well level.
* The **Activities** view keeps track of all activities performed for the Screen, including both the screening visits and service activities performed.

A **Study** is similar to a screen, except that the reagents and the data associated with the study are based on publications or other research data and not on a screening assay performed at the facility. 

## Create a new screen

To create a screen, use the "Add screen" button on the bottom of the left panel.

When a new screen is created, it is assigned the next available **Screen Facility ID**.

Important fields:
* **Principal Investigator** the lab head for the lab sponsoring this screen
* **Lead Screener** the researcher conducting this screen
* **Collaborators** other researchers associated with this screen
* **Status** All screens begin with the "accepted" status
* **Comments** visible only to staff
* **Data sharing level** All screens must have a **Data sharing level** assigned. See [Data sharing rules](../reference.html#iccb-l-screener-data-sharing-rules) for more information.

* Before data are deposited, screens will only be visible to Screen members (the Principal investigator, lead screener, or collaborators).

## Library screening visits

When screens are conducted at the facility, the plates of one or more library copies are used to produce the assay plates used for screening. The usage of library copy plates is tracked in Screensaver by adding a new **Library Screening activity**. 

Each library screening activity tracks:
* the set of library copy plates that were used to produce the screening assay plates,
* the volume of reagent that was taken from each library copy well of the copy plates,
* the number of replicate assay plates that were created.

This information is used to keep track of the number of times each copy has been used as well as the total consumed and remaining reagent volume of every library copy plate. 

To add a new library screening visit, go to the "Activities" tab of the Screen, and use the "Add library screening visit" button.

## How to find available library copy plates for screening

The [Screening inquiry form](search-utilities.html#screening-inquiry), accessed from the left hand search box, facilitates searches for sets of library copy plates.

## Recording service activities

**Service Activities** record the different tasks that staff will perform when administering a HTS screening assay. 

To add a new service activity, go to the "Activities" tab of the Screen, and use the "Add library service activity" button.

## Upload screen result data

After the screening assay has been performed, the result data for this assay may be formatted and uploaded to the Screensaver database.

See [Screen Result File Format](screenresult-file-format.html)

## Raw data transformation

Screening assay result data are detected by different **plate reader** devices. These devices may produce the **raw data** results in different formats including text or CSV.

The **Raw Data Transformer** utility in Screensaver may be used to parse these raw data results, and to collate read-out types, replicates and conditions that are measured, and to associate these collated results with plate and well data from the screensaver database. The Raw Data Transformer output can then be entered into the [Screen Result File Format](screenresult-file-format.html).

see [Raw Data Transformer](raw-data-transformer.html) for details.

## Recording "cherry pick" or "follow-up" reagent requests 

When anaylizing the screen results for an experimental assay, specific reagents may be identified as significant and selected for follow-up assays. "Cherry picking" is term used for this selection process.

To create a **Cherry Pick Request**, select the "Cherry picks" tab on the screen page, and then use the "add" button.

For details on the cherry pick request process, see [Cherry Pick Request](cherry-pick-request.html)

# Create a study (in-silco screen)

A **Study** is similar to a **Screen** in that it is used to associate data with reagents by well in the Screensaver libraries. 

The "Add study" button is located at the bottom of the left menu panel. 

In "Study Details"
* The "Study ID" should be created by adding 1 to the existing study with the highest number.
  * at ICCB-L, the "100,000" range of ID values are used for normal studies, and the "200,000" range of ID values are reserved for automatically generated studies. 
  * The Study ID may not be changed after creation.
* "Title" and "Summary" are free text, required fields
  * Title, Lab Name, and Summary can be edited after study creation.
* "Library Screen Type", "Lab Name", and "Study Type" have defined values for selection. 

Following creation of a study, data can be uploaded using an Excel (.xlsx) in the same format as loading screen results. This is done using the "Load data" button in the Data section. 
* Required fields are "plate_number" and "well_name". 
* One or more data columns are then defined that will display the study data

See [Screen Result File Format](screenresult-file-format.html) for more details on this process.
