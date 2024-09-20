----
----
### Active Directory Terminology

-------
----

Before going further, we should determine some keywords related to Active Directory that will be useful during our journey.

#### Objects :

An **`object`** defines ANY resource you can find in an Active Directory environment. It can be users, printers, domains etc...

#### Attributes :

Every `object` of the AD has a set of values named **`attributes`** used to define the characteristics of the given `object`.

#### Domains :

A **`domain`** is a logical group of objects (such as computers, users etc) linked between them. We can compare each domain of a `forest` to different cities in a same state or country.

#### Forests :

A **`forest`** is a collection of Active Directory `domains`. It is the topmost container and gathers all of the AD `Objects` listed bellow. We also can compare a `forest` with a state in the US.

#### Global Unique Identifier (GUID) :

A **`GUID`** is a unique 128-bit value assigned when a domain user or a group is created. It is similar to mac addresses, meaning that each GUID is unique all around the world and created by AD. We can access to this value when requesting any `Object` in an AD environment with PowerShell with the `objectGUID` value. it is probably the most accurate technique to search an `Object` within the AD.

#### Distinguished Name (DN) :

A **`DN`** describes the full path to an object in AD (such as `cn=bjones, ou=IT, ou=Employees, dc=inlanefreight, dc=local`). In this example, the user `bjones` works in the IT department of the company Inlanefreight, and his account is created in an Organizational Unit (OU) that holds accounts for company employees. The Common Name (CN) `bjones` is just one way the user object could be searched for or accessed within the domain.

#### sAMAccountName : 

The **`sAMAccountName`** is the user's logon name. Here it would just be `bjones`. It must be a unique value and 20 or fewer characters.

#### userPrincipalName :

The **`userPrincipalName`** attribute is another way to identify users in AD. This attribute consists of a prefix (the user account name) and a suffix (the domain name) in the format of `bjones@inlanefreight.local`. This attribute is not mandatory.

#### Service Principal Name (SPN) :

A **`SPN`** uniquely identifies a service instance. They are used by Kerberos authentication to associate an instance of a service with a logon account, allowing a client application to request the service to authenticate an account without needing to know the account name.

#### Group Policy Object (GPO) :

**`GPO`** are virtual collections of policy settings. Each GPO has a unique `GUID`. A GPO can contain local file system settings or Active Directory settings. GPO settings can be applied to both user and computer objects. They can be applied to all users and computers within the domain or defined more granularly at the OU level.

#### Fully Qualified Domain Name (FQDN) :

An **`FQDN`** is the complete name for a specific computer or host. It is written with the hostname and domain name in the format [host name].[domain name].[tld]. This is used to specify an object's location in the tree hierarchy of DNS. The FQDN can be used to locate hosts in an Active Directory without knowing the IP address, much like when browsing to a website such as google.com instead of typing in the associated IP address. An example would be the host `DC01` in the domain `INLANEFREIGHT.LOCAL`. The FQDN here would be `DC01.INLANEFREIGHT.LOCAL`.