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

To create a new library, use the "Add library" button on the bottom of the left panel. When creating a new library, define the plate type, and the number of plates that will be used in the library. On creation, the system initialize each well of the created plates with the "undefined" placeholder. After the library has been created, well definitions can be uploaded.

## Upload library well definitions

To upload library well definitions, use the "Upload" button on the library details tab.

See [Library File Formats](library-file-formats.html) for further details on this process.

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




