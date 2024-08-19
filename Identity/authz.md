# <center>Authorization</center>

<br></br>



## What
Authorization is all about giving access to a verified identity, what they should have access to. The tracking and enforcing that access and usage. With authorization you focus on:

* Entitlement Type - Entitlements focus on whether or not an identity has been granted (“entitled”) access to particular resource. The assignment of entitlements happens at app level, centrally via groups, defined through RBAC or ABAC or applied centrally using PBAC approach.
* Access Policies It focus on a set of app, data, and which users can perform activities. Think of it as the set of rules around getting your job done. Focus on the least access you need.
* Enforcement - It focuses on how org handles the enforcement of authorization activities. In most cases, org handle enforcement at app layer. Meaning enforcement is completed by API within app itself. Some forms of enforcement consist of the use a reverse proxy to externalize authorization enforcement. A current trend is to use an external policy source to determine how identity interacts with resource.

Common types of authorization approaches:
* Access Control Lists (ACLs) - An explicit list of specific entities who do or don't have access to a resource.
* Role-based access control (RBAC)
* Attribute-based access control (ABAC) - Rules are applied to attributes of entity, resources being accessed, and the current environment to determine whether access to some resources or functionality is permitted. An example might be only allowing users who are managers to access files identified with a metadata tag of “managers during working hours only” during the hours of 9AM - 5PM on working days. In this case, access is determined by examining the user’s attribute (status as manager), the resource’s attribute (metadata tag on a file), and also an environment attribute (the current time).
* Policy-based access control (PBAC) - A strategy for managing user access to systems, where the business-role of user is combined with policies to determine what access the user has.

<br></br>
