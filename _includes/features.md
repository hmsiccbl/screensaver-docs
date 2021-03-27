## Features

* Libraries
  * Manage screening libraries, including small molecule and RNAi libraries.
  * Import library plate/well contents from SD and Excel files.
  * Browse and search library contents (well and reagent information).
  * View small molecule structures.
  * Track, view, and set well reagent volumes on library plate copies, ensuring source library plate copies are never overdrawn.
  * Create and track library copies, including the status and storage locations of all library copy plates.
  * Track library copy screening statistics.
  * Track library copy well screening and cherry pick statistics.
* Screens
  * Manage screens and screen result data.
  * Manage relevant screen information, such as title, PI, collaborators, assay protocol, status, publications, etc.
  * View and export screen result data in sortable and searchable data tables.
  * Perform side-by-side data comparisons between multiple screens.
  * Cross-screen hit comparisons, allowing comparison and analysis of mutual "positives" betweens screens.
  * Management of follow-up screens and hit confirmation results.
  * Group together related screens by project.
* Activities
  * Track library plate screenings, cherry pick plate creations, and data-related administrative activities. 
* Cherry Pick Requests
  * Manage screener requests to produce cherry pick plates used to perform follow-up confirmation (validation) screens.
  * Locate optimal library plate copies from which to pick requested reagent volumes.
  * Maintain a copy-well level record of volume and freeze/thaw cycles.
  * Manage the workflow for producing cherry pick plates, tracking the status.
  * Generate machine-readable plate mapping files for use by automated plate mapping machines.
* Studies
  * Add annotations to library reagents, allowing biologically relevant information to be shared among all users. 
  * For example, cell toxicity or luminescence data on small molecule reagents, siRNA off-target effects, etc. 
  * Annotation data can be provided as part of an imported screen result or can be imported from the data of an external, published study.
* Manage roles and permissions for staff
  * Manage permissions on a API resource and field level for users and groups.
  * Define permission roles by capability to read or write to API resources or fields.
  * Define role permission inheritance.
  * Compose user groups from individuals or other groups. 
* Screener User Management
  * Maintain screeners' associations with fellow lab members and screen collaborators
  * Track screeners' administrative details via "checklist items" (e.g., to track required trainings, email list subscriptions, etc.)
  * Support for multiple data sharing levels for screeners's data.  This includes tiered levels of mutual sharing, so that screeners can view data from others' screens that are being shared at the same level. (This encourages screeners to share their data, but still supports the option of full data privacy.)
* Searchable logs
  * Diff logs for all changes are stored in a searchable database
  * History log is browsable from each record.
* Metadata driven design
  * API schema Resource and Field definitions are stored in the database.
  * Support for reuse of metadata definitions through inheritance.
  * Manage field display properties such as title, description, ordering, and formatting.
  * Control field visibility, editability, and permissions.
  * Use metadata definitions to facilitate diff logging and historical auditing.
* Job Control
  * Offloads long running jobs to subprocesses so that the browser remains responsive.
  * Track job progress and record of job output.
  * State management for long running jobs; including cancellation and failure status reporting.
* Permanent and shareable URLs
  * Facilitate collaboration between users using stable URLs.
  * Return to a browser location and state after logout.
