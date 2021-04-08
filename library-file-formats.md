---
layout: default
title: Library File Formats 
nav_order: 4
parent: Administration
---

# Library File Formats



## Small Molecule Library

Data may be loaded using XLSX, CSV, or SDF format.

Chemical structure information (molfile) requires the [SDF Format](https://en.wikipedia.org/wiki/Chemical_table_file#SDF)


### Fields for upload

| *Data Field* | *Is Required?* | *Format* | *Multi* |
|---|---|---|---|
| Plate | yes | positive integer | no |
| Well | yes | letter A-P, followed by a number 1-24 (assumes 384-well plates) | no |
| Well_type | yes | one of ["EXPERIMENTAL","EMPTY","DMSO"] | no |
| Vendor | yes | text | no |
| Vendor_Reagent_ID | yes | text | no |
| Facility_Reagent_ID | no | text | no |
| Vendor_Batch_ID | no | text | no |
| Facility_Batch_ID | no | integer | no |
| Salt_Form_ID | no | integer | no |
| SMILES | no | text | no |
| !InChi | no | text | no |
| Molecular_Formula | no | text, see below | no |
| Molecular_Mass | no | real number, up to 9 decimal places, 15 digits total | no |
| Molecular_Weight | no | real number, up to 9 decimal places, 15 digits total | no |
| Chemical_Name | no | text | yes |
| !PubMed_ID | no | positive integer | yes |
| !PubChem_CID | no | positive integer | yes |
| !ChemBank_ID | no | positive integer | yes |
| !ChEMBL_ID | no | positive integer | yes |
| Concentration | yes | concentration | yes, if experimental well, optional otherwise.  see format below. |

Molecular Formula fields accept any text.  However, when these formulas are displayed, note that integer values following letters or parentheses will be shown as subscripts.  A plus or minus sign (+, -), followed by an optional integer value will be shown as a superscript, with the sign and value transposed (intended for ion charges).  

Concentration values may be formatted as:
   * ###.### mM
   * ###.### uM
   * ###.### nM
   * ###.### pM
   * ###.### mg/ml
