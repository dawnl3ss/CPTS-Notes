---
---
---
---
### Active Directory Functionality

---
---

#### Trusts

A trust is used to establish `forest-forest` or `domain-domain` authentication, allowing users to access resources in (or administer) another domain outside of the domain their account resides in. A trust creates a link between the authentication systems of two domains.

There are several trust types.

| **Trust Type** | **Description**                                                                                                                                                        |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Parent-child` | Domains within the same forest. The child domain has a two-way transitive trust with the parent domain.                                                                |
| `Cross-link`   | a trust between child domains to speed up authentication.                                                                                                              |
| `External`     | A non-transitive trust between two separate domains in separate forests which are not already joined by a forest trust. This type of trust utilizes SID filtering.     |
| `Tree-root`    | a two-way transitive trust between a forest root domain and a new tree root domain. They are created by design when you set up a new tree root domain within a forest. |
| `Forest`       | a transitive trust between two forest root domains.                                                                                                                    |

<img src="https://academy.hackthebox.com/storage/modules/74/trusts-diagram.png">

Trusts can be transitive or non-transitive.

- A transitive trust means that trust is extended to objects that the child domain trusts.
- In a non-transitive trust, only the child domain itself is trusted.

Trusts can be set up to be one-way or two-way (bidirectional).

- In bidirectional trusts, users from both trusting domains can access resources.
- In a one-way trust, only users in a trusted domain can access resources in a trusting domain, not vice-versa. The direction of trust is opposite to the direction of access.


#### Conclusion :

Often, domain trusts are set up improperly and provide unintended attack paths. Also, trusts set up for ease of use may not be reviewed later for potential security implications. Mergers and acquisitions can result in bidirectional trusts with acquired companies, unknowingly introducing risk into the acquiring company’s environment. It is not uncommon to be able to perform an attack such as Kerberoasting against a domain outside the principal domain and obtain a user that has administrative access within the principal domain.


02/08/2025,  
Dawnless.

--------------------------------------------
--------------------------------------------