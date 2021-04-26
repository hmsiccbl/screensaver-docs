---
layout: default
title: User Management
nav_order: 6
parent: Administration
---
{: .no_toc }

1. TOC
{:toc}
---


# User Management
Use the "Add user" button on the bottom of the left panel to add a new user account to the system.

### User  Account type

A User account (record) may be marked as a "Staff"; otherwise the user record is a "Screener" account.
* **Staff** accounts may be assigned read and write permissions on resources and fields.
  * Permissions are managed by assigning users to groups and permissions to the group.
* **Screener** accounts are for the individuals who will use the screening facility to conduct experiments.
  * Permissions are managed by the data sharing rules that have been implemented for the facility.

### User classification

The user classification identifies the role of the Screener in the experiments:
* **Principal Investigator** classification is reserved for user accounts that will be designated as the Principal Investigator for Screens (experiments).
  * Principal Investigator accounts may have lab members assigned.
* Other **non-staff classifications** identify non-PI screener accounts.
  * non-PI screener accounts must be assigned as a "lab member" to a PI user account.
* **Staff classifications** are reserved for administrative user accounts.

### Assign a username

In order to be able to log in, the new user account must be assigned a User ID.
* ICCB-L specific accounts should be assigned an **Ecommons ID** - this will server as the username.
* Other accounts should be assigned a **Username**.
  * Note: Screensaver does not provide an interface for direct management of user passwords. The ICCB-L Authorization system (TODO: link) provides a mechanism to proxy the user login action to the Harvard Ecommons system.
  * The [Django Admin Interface](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/) may be used by administrative accounts to set user passwords.

### Set the user data sharing level

For screener accounts created on systems using the ICCB-L authorization implementations, a data sharing level must be assigned to these accounts after creation in order for the account to be "active" (allowing log in).
