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

* Volume requested and approved and the staff member approving the request
  * the **Approved by** drop down list is populated by all users identified as **staff**.
* Keep source cherry pick plates together
* Random plate well layout
* Wells to leave empty
* Assay protocol

## Screener Cherry Picks

Based on analysis of the primary screen, the experimentalist (the "screener") may identify specific wells as significant. These wells are entered on the **Screener Cherry Picks** tab entry form. 
* Screensaver will show the plate and well information for the for the requested wells - be sure to verify that the number of wells located matches the number of wells that were entered in the search.
  * If the search was unsuccessful, select **Delete screener cherry picks** and try again
* Other reagents

## Lab Cherry Picks

The Screensaver system will use the **Screener cherry picks** to search for physical **library copy plates** where the **copy wells** have sufficient volume to be used to create the follow-up assay plates.

Lab Cherry Pick selection process



## Cherry Pick Plates (follow-up assay plates)

After the lab cherry pick source copy wells have all been successfully located ("fulfilled"), select **Reserve selections and map to plates**. Screensaver will generate the follow-up assay plates according to the settings specified, and volume subtractions will be recorded for each copy-well volume.

## Transforming raw data from the follow-up assay

see [Raw Data Transformer](raw-data-transformer.html)
