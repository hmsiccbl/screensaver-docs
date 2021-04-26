---
layout: default
title: Reference
nav_order: 7
has_children: true
---
# Screensaver Reference Topics
{: .no_toc }

1. TOC
{:toc}
---


# ICCB-L Screener Data Sharing Rules

Data access permissions for screener accounts at the ICCB-L are defined by data sharing agreements. 

* Small molecule Screen data sharing is defined in the [ICCB-L Small Molecule User Agreement](https://iccb.med.harvard.edu/files/iccb/files/iccbl_sm_user_agreement_sept2017.pdf)
* Functional genomics Screen data sharing is defined in the [ICCB-L Functional Genomics User Agreement](https://iccb.med.harvard.edu/files/iccb/files/iccbl_functionalgenomics_ua_may2020.pdf)


## Effective User-Screen Data Access Levels

Screensaver determines the visibility of Screen data to a Screener by calculating the "Effective User-Screen Data Access Level" for each Screener user with each Screen.

(permissions for each level include all lower level permissions)

Level | Viewing permissions
--- | --- 
0 | Screen "general" details: Title, Screen members
1 | Publishable Protocol Field, Summary Field, Overlapping Hits (visible in own Screen Result section), Only data for overlapping rows of the overlapping screens results
2 | Positives summary, Screen summary, Full screen results
3 | "Full" visibilty of the screen details

## User-Screen Data Access Level Matrix
( for users with qualifying data deposited)

Other Screen DSL ==><br>**⇩** User DSL | Own Screens | 0 (Published) | 1 | 2 | 3 
---| ---| --- | --- | --- | --- 
1 | Data Access Level 3 | Data Access Level 2 | Data Access Level 2, if both user and screen have data deposited | Data Access Level 1 if overlapping hit,0 otherwise | No access
2 | Data Access Level 3 | Data Access Level 2 | Data Access Level 1 if overlapping hit, 0 otherwise | Data Access Level 1 if overlapping hit, 0 otherwise | No access
3 | Data Access Level 3 | Data Access Level 2 | No access | No access No access




# ICCBL Authorization implementation

The Authorization classes that are assigned by default are set up for the ICCB-L Screening Facility. These assignments are as follows.

**UserGroupAuthorization**
The default class controlling Staff user permissions. Authorize users based on User and Group assigned permissions.

**LibraryResourceAuthorization**
* Write permission is determined using UserGroupAuthorization.
* Read permission is granted to all authenticated users.
  * Only Staff may view Libraries that are not "released"

**ReagentResourceAuthorization**
* For Well and Reagent views
* Same permission assignents as LibraryResourceAuthorization

**ScreenAuthorization**
* Control access to Screen and Study Resources
* Override UserGroupAuthorization to give screeners permission for restricted read access to screens they are authorized to view.
  * Screener authorization is determined by the [ICCB-L Data Sharing Rules](#iccb-l-screener-data-sharing-rules)

**ScreenResultAuthorization**
* Control screener access to screen result data as defined by [ICCB-L Data Sharing Rules](#iccb-l-screener-data-sharing-rules)

**DataColumnAuthorization**
* Control screener access to screen data column information as defined by [ICCB-L Data Sharing Rules](#iccb-l-screener-data-sharing-rules)

TODO: How to override default authorization with AllAuthenticatedWriteAuthorization (Or AllAthenticatedStaffWriteAuthorization) for ScreenResource, LibraryResource, etc...


# Request Background Processing

Many HTTP Requests can require more time than the HTTP server will allow to process the request before streaming a response back to the client. Such requests are handled as "background jobs" by Screensaver. 

## Background process sequence
* When the server recieves a background job request
  * a Job entry is created and a Job ID is returned immediately to the client. 
  * Simultaneously, the server will fork a subprocess on the webserver operating system. 
* This subprocess will spin up a separate special server instance and recreate the request on to this instance. 
  * This special server instance will record status to the Job entry, and 
  * will write the request response to the filesystem when finished. 
* At any time after the initial request, the client may query the Job status using the Job ID.
* when the Job status is complete, the stored response may be retrieved.

## Background processing settings

```
    BACKGROUND_PROCESSING = True
    APP_PUBLIC_DATA.BACKGROUND_PROCESSING = BACKGROUND_PROCESSING

    BACKGROUND_PROCESSOR = {
        SCHEMA.SETTINGS.BACKGROUND.POST_DATA_DIR: os.path.join(
            PROJECT_ROOT, "..", "logs", "background", "post_data"
        ),
        SCHEMA.SETTINGS.BACKGROUND.JOB_OUTPUT_DIR: os.path.join(
            PROJECT_ROOT, "..", "logs", "background", "job_output"
        ),
        SCHEMA.SETTINGS.BACKGROUND.RESPONSE_DATA_DIR: os.path.join(
            PROJECT_ROOT, "..", "logs", "background", "response_data"),
        SCHEMA.SETTINGS.BACKGROUND.RESPONSE_DATA_DIR_MAX_BYTES: (2**30)*1, # 1GB
        SCHEMA.SETTINGS.BACKGROUND.MAX_JOBS_PER_PERSON: 3,
        "credential_file": os.path.join(
            PROJECT_ROOT, "..", "production_data", "credentials.txt"
        ),
        "python_environ_script": os.path.join(PROJECT_ROOT, 'scripts', "run_webconf_consolelogs.sh"),
        "background_process_script": "reports.utils.background_client_util",
        }
```


# Screener User Manual

For usage of the Web client application, see the [Screener User Manual](https://iccb.med.harvard.edu/files/iccb/files/ss2_usermanual_12042018.pdf).

