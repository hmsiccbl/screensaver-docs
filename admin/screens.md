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

## Screen and Study Management

A screen tracks the progress of performing a screening assay, including a description of its biological significance, its experimental protocol, and additional data to support the administrative needs of the facility. After screening data is generated, this data may uploaded and associated with the screen record.

A study is similar to a screen, except that the reagents and the data associated with the study are based on publications or other research data and not on a screening assay performed at the facility. 

### Create a new screen

To create a screen, use the "Add screen" button on the bottom of the left panel.

### Record a library screening visit

When screens are conducted at the facility, the plates of one or more library copies are used to produce the assay plates used for screening. The usage of library copy plates is tracked in Screensaver by adding a new **Library Screening activity**. Each library screening activity tracks the set of library copy plates that have been used, along with the volume of reagent that was taken from each library copy well and the number of assay plate replicates that were produced. In this way, the Screensaver database can be used calculate the number of times each copy has been used as well as the total consumed and remaining reagent volume of every library copy plate. 

To add a new library screening visit, go to the "Activities" tab of the Screen, and use the "Add library screening visit" button.

see [Library screening visit](library-screening.html)

### Recording service activities

**Service Activities** record the different tasks that staff will perform when administering a HTS screening assay. 

To add a new service activity, go to the "Activities" tab of the Screen, and use the "Add library service activity" button.

### Upload screen results

After the screening assay has been performed, the results of this assay may be formatted and uploaded to the Screensaver database.

See [Screen Result File Format](screenresult-file-format.html)

### Raw data transformation

Screening assay result data are detected by different **plate reader** devices. These devices may produce the **raw data** results in different formats including text or CSV.

The **Raw Data Transformer** utility in Screensaver may be used to parse these raw data results, and to collate read-out types, replicates and conditions that are measured, and to associate these collated results with plate and well data from the screensaver database. The Raw Data Transformer output can then be entered into the [Screen Result File Format](screenresult-file-format.html).

see [Raw Data Transformer](raw-data-transformer.html) for details.

### Recording "cherry pick" or "follow-up" reagent requests 

When anaylizing the screen results for an experimental assay, specific reagents may be identified as significant and selected for follow-up assays. "Cherry picking" is term used for this selection process.

To create a "cherry pick request", select the "Cherry picks" tab on the screen page, and then use the "add" button.

For details on the cherry pick request process, see [Cherry Pick Request](cherry-pick-request.html)

### Create a study (in-silco screen)

A **Study** is similar to a **Screen** in that it is used to associate data with reagents in the Screensaver libraries. Therefore, the study data are formatted in an identical manner to the Screen result data and are uploaded in the same way.

See [Screen Result File Format](screenresult-file-format.html) for more details on this process.
