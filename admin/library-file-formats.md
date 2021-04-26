---
layout: default
title: Library File Formats 
nav_order: 11
parent: Library Management
grand_parent: Administration
---

# Library File Formats

The file formats for library data follow the same guidelines as for any other resource of the Screensaver API. These guidelines are explained in [data interchange](../reference/data-interchange.html).


## Small Molecule Library

Data may be loaded using XLSX, CSV, or SDF format.

Chemical structure information (molfile) requires the [SDF Format](https://en.wikipedia.org/wiki/Chemical_table_file#SDF)

## Key fields

All library data uploads must define either a **plate_number** and **well_name** or alternatively, a **well_id**.
** The plate_number corresponds to a plate of the library,
** The well_id is the combination of the plate_number and the well_name.

### General fields for upload

| *Data Field* | *Is Required?* | *Format* | *Multi* |
|---|---|---|---|
| plate_number | yes | positive integer | no |
| well_name | yes | letter A-P, followed by a number 1-24 (assumes 384-well plates) | no |
| well_id | yes | required if plate_number and well_name are not provided | no |
| well_type | yes | one of ["experimental","empty","dmso"] | no |
| vendor | yes | text | no |
| vendor_reagent_id | yes | text | no |
| vendor_batch_id | no | text | no |
| facility_id | no | text | no |
| molar_concentration | yes, if experimental well, optional otherwise.  see format below. | concentration |  |
| mg_ml_concentration | yes, if experimental well, optional otherwise.  see format below. | concentration |  |
| is_deprecated | no | boolean | no |
| deprecation_reason | no | text | no |


### Small molecule fields for upload

| *Data Field* | *Is Required?* | *Format* | *Multi* |
|---|---|---|---|
| smiles | no | text | no |
| InChi | no | text | no |
| molecular_formula | no | text | no |
| molecular_mass | no | real number, up to 9 decimal places, 15 digits total | no |
| molecular_weight | no | real number, up to 9 decimal places, 15 digits total | no |
| compound_name | no | text | yes |
| pubmed_id | no | positive integer | yes |
| pubchem_cid | no | positive integer | yes |
| chembank_id | no | positive integer | yes |
| chembl_id | no | positive integer | yes |

### Functional genomics fields for upload

| *Data Field* | *Is Required?* | *Format* | *Multi* |
|---|---|---|---|
| silencing_reagent_type | yes | text | yes |
| sequence | yes | text | no |
| anti_sense_sequence | yes | text | no |
| vendor_gene_name | yes | text | no |
| vendor_entrezgene_id | yes | integer | no |
| vendor_entrezgene_symbols | yes | text | yes |
| vendor_genebank_accession_numbers | yes | text | yes |
| vendor_species_name | yes | text | no |
| facility_gene_name | no | text | no |
| facility_entrezgene_id | no | integer | no |
| facility_entrezgene_symbols | no | text | yes |
| facility_genebank_accession_numbers | no | text | yes |
| facility_species_name | no | text | no |
| is_pool | no | boolean | no |
| duplex_wells | no | text | yes |
| is_restricted_sequence | no | boolean | yes |


### Concentration values may be formatted as:
   * ###.### mM
   * ###.### uM
   * ###.### nM
   * ###.### pM
   * ###.### mg/ml
