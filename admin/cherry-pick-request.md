---
layout: default
title: Cherry Pick Requests
nav_order: 13
parent: Screen Management
grand_parent: Administration
---
{: .no_toc }

1. TOC
{:toc}
---


# Cherry Pick Requests

When anaylizing the screen results for an experimental assay, specific reagents may be identified as significant and selected for follow-up assays. "Cherry picking" is term used for this selection process.

To create a **Cherry Pick Request** select the "Cherry picks" tab on the screen page, and then use the "add" button.

## General setup

* Date requested and requested by (defined list based on screen PI, lead screener, and collaborators)
* Volume requested and approved and the staff member approving the request
the Approved by drop down list is populated by all users identified as staff.
* Keep source cherry pick plates together - initially set as "True", which keeps all wells from a source plate on the same cherry pick plate
* Random plate well layout - initally set as "False", and ompounds will be arrayed from low to high well_id starting at the first available well at the top and moving down columns
* Wells to leave empty - use the well picker visual tool to modify the plate format from the default outer two rows and columns left empty
* Assay protocol - used to indicate whether cherry pick will repeat the primary screen assay or follow a new protocol

## Screener Cherry Picks

Based on analysis of the primary screen, the experimentalist (the "screener") may identify specific wells as potential positives. These wells are entered on the **Screener Cherry Picks** tab entry form. 

* Screensaver will show the plate and well information for the for the requested wells - be sure to verify that the number of wells located matches the number of wells that were entered in the search. If wells need to be changed, check show "Other Reagents" and change the selected wells. This may be necessary, for example, if requested wells in multi-concentration libraries are not 10mM.
  * If the search was unsuccessful, select Delete screener cherry picks and try again. This may be necessary when invalid wells have been input (non-experimental library wells, duplicates, or invalid well names) and a corrected list needs to be submitted.

## Lab Cherry Picks

The Screensaver system will use the **Screener cherry picks** to search for physical **library copy plates** where the **copy wells** have sufficient volume to be used to create the follow-up assay plates.

Lab Cherry Pick selection process



## Cherry Pick Plates (follow-up assay plates)

After the lab cherry pick source copy wells have all been successfully located ("fulfilled"), select **Reserve selections and map to plates**. Screensaver will generate the follow-up assay plates according to the settings specified, and volume subtractions will be recorded for each copy-well volume.

## Transforming raw data from the follow-up assay

see [Raw Data Transformer](raw-data-transformer.html)
