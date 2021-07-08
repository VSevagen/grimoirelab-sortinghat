---
layout: default
title: Troubleshoot
nav_order: 5
parent: SortingHat
---

# Troubleshooting steps

### Login Issues

<img src="../../../assets/sortinghat/sortinghat-invalid-credentials.png" alt="sortinghat-invalid-credentials" style="display: block; margin-left: auto; margin-right: auto;" />

This error is pretty straightforward. You have either mistyped your username and password or you have forgotten your credentials.
Usually that would not happen since SortingHat uses cookies to improve user experience. But in the case that you've logged out, here's how to regain access.

Assuming that you did not forget your username, you can use the following command to change your password.

```
poetry run python manage.py changepassword <user_name> --settings=config.settings.devel
```

In the case that you forgot your username as well, you can check out your database server(MySQL or MariaDB) and look into the `sortinghat_db` database. The `auth_user` table contains data pertaining to login credentials. The password is encryped but the username is readable. Once you've got hold of the username, follow the above step to change your password.

### Profile creation issues

<img src="../../../assets/sortinghat/sortinghat-orgs.png" alt="sortinghat-orgs" style="display: block; margin-left: auto; margin-right: auto;" />

The above issue arises when the organisation submitted does not exist in the `Organisation` table. "Bitergia" here is taken as an example.
In order to fix it, make sure to [add your organisation](http://localhost:4000/docs/sortinghat/add-org/) first, then [create the individuals profile](http://localhost:4000/docs/sortinghat/create-profile/).<br>

<img src="../../../assets/sortinghat/sortinghat-sameIdentity.png" alt="sortinghat-sameIdentity" style="display: block; margin-left: auto; margin-right: auto;" /><br>
The above issue arises if a existing profile has the exact same information (Name, Email, Username, Source etc...) as the profile being created. The ID `013d8db4d7fba708448c146c8fb54f8dcb974ed1` refers to the unique identifier of a profile.

<img src="../../../assets/sortinghat/sortinghat-no-identity.png" alt="sortinghat-no-identity" style="display: block; margin-left: auto; margin-right: auto;" /><br>
The above issue is pretty staightforward. In order to create a profile, a minimum amount of information is required which includes, primarily the <code>Source</code> and any other identity related info (`Name` or `Email` or `Username`).
