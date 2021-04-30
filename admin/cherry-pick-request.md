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

* "Date requested" and "Requested by" are required (defined list based on screen PI, lead screener, and collaborators)
* "Volume requested", "Volume approved" and "Approved by" (the staff member approving the request - populated by all users identified as staff).
* "Keep source cherry pick plates together" 
  * if "true", Screensaver will leave blank wells on the destination plate if necessary to keep all of the sourced wells from a copy plate together, 
  * if "false", then Screensaver will leave no blank wells wells on the destination plates and may split source wells from a source copy plate onto two destination plates (this may make lab automation harder because source plates will have to be loaded twice). 
* Random plate well layout
  * if "true", compounds will be arrayed in random order on the destination plates
  * if "false", compounds will be arrayed from low to high well_id starting at the first available well at the top and moving down columns.
  * Note that this setting has no effect on the "Keep source cherry pick plates together" setting.
* Wells to leave empty - use the well picker visual tool to specify wells to leave empty on the destination cherry pick assay plates
* Assay protocol - indicate whether cherry pick will repeat the primary screen assay or follow a new protocol

## Screener Cherry Picks

Based on analysis of the primary screen, the experimentalist (the "screener") may identify specific wells as potential positives. 

1. Enter the desired well IDs in the **Screener Cherry Picks** tab entry form
  * Entries may be separated by comma, space, or newline. 
2. Screensaver will show the plate and well information for the for the requested wells.
  * Be sure to verify that the number of wells located matches the number of wells that were entered in the search. 
3. If wells need to be changed, check show "Other Reagents" and change the selected wells.
  * This may be necessary, for example, if requested wells in multi-concentration libraries are not of the desired concentration (e.g. 10mM are shown, but 5mM are desired).
4. If the search was unsuccessful, select Delete screener cherry picks and try again. 
  * This may be necessary when invalid wells have been input (non-experimental library wells, duplicates, or invalid well names) and a corrected list needs to be submitted.

## Lab Cherry Picks

Once the **Screener cherry picks** are selected and finalized, suitable **copy wells** that have sufficient volume must be located. When a suitable **copy well** is chosen, this copy well is referred to as a **Lab cherry pick**.

Screensaver will search for lab cherry picks using the following rules:
* Library copy type: "Cherry Pick Source Plates"
* Library copy plate status: "Active"
* Volume for the well is greater than the minimum allowed vol + requested volume
  * For small molecule libraries, the minimum volume is 6.9 uL
  * For functional genomic libraries, the minimum volume is 0 uL

Lab Cherry Pick selection process

1. Use the "Set lab cherry picks" button on the "Screener cherry picks" tab.
  * "Find a minimal set of copies" - with this option, Screensaver will try to select all of the lab cherry picks for a plate from the same library copy plate. In this way, fewer plates will need to be pulled and thawed from storage, but over time, more "pristine" or unused copy plates will be used, and copy plates will not be depleted as efficiently,
  * "Use the first available copy" - with this option, Screensaver will select the lab cherry picks from the "first" (by alphabetical sort) available copy having sufficient volume for that well, and may result in more copy plates being required, but in practice will result in more even depletion of the library copy plates over time.
2. Screensaver will report the number of "unfulfilled" screener cherry picks for the process
  * a pick is "unfulfilled" if no "available", "Cherry Pick Source Plate" can be found.
3. Resolve "unfulfilled" picks
  * Staff discretion may be used to locate unfulfilled picks from "retired" "Library Screening Plates"
  * To facilitate this process, select the show "Available and Retired" option in the report view.
  * Alternate "retired" "Library Screening Plate" copies will be shown, staff may then select from these and save the selections.
  * After selecting, these manually selected picks may be shown using the show "Manually selected" option.

## Reserving selections and mapping to plates

Once all unfulfilled screener cherry picks have been resolved, the lab cherry picks can be "reserved" by the system and then the destination cherry pick assay plate layouts can be generated.
* Once a pick is reserved, the volume removal will be recorded to the system and the a freeze/thaw record will be created for the library copy plate.

To reserve, select the "Reserve selections and map to plates" option.

## Undoing reservations and lab cherry pick selections.

After volumes have been reserved, it is possible to undo the volume depletion and the freeze/thaw record, using the "Cancel reservation and delete plating assignments" button.
* Note that once a reservation is cancelled, there will be no record of the plate layout that was generated. Therefore, this option may not be used to swap one lab cherry pick selection for another, because the new plate layout may not match the old plate layout.
* For this reason, it is important to verify the lab cherry pick selections before reserving them in the system.
  * This is relevant if the recorded volumes in the system are inaccurate and must be visually verified. 

## Cherry Pick Plates (follow-up assay plates)

After reserving the selections, the destination cherry pick assay plate layout can be viewed from the "Cherry Pick Plates" tab.
* Use the "Download plate mapping files" to generate a zip file containing plate location and the specific information aligning source well locations to destination well locations. 
* This information may be used to create instructions for automated pin transfer tools.

## Transforming raw data from the follow-up assay

see [Raw Data Transformer](raw-data-transformer.html)
