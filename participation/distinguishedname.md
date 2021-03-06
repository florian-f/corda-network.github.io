|Corda Network|[Document history]({{ site.github.repository_url }}/blame/master/{{page.path}})|

Choosing your node's Distinguished Name
=======================================

Any node on Corda Network must have a Distinguished Name (DN) in its [participation certificate](https://docs.corda.net/corda-network/index.html#identity-service). The DN must, at minimum, have 3 fields included (Organisation (O), Locality (L), Country (C)). It may include up to 6 fields (optional 3 additional fields are: Organisation Unit (OU), State (S), and Common Name(CN)). These 6 fields are explained below. 

A DN must be unique within Corda Network. Only O and OU are used for the identity uniqueness check, and the other fields are considered as attributes of the identity. 

All data fields must adhere to the following constraints:
* Only uses Latin, common and inherited unicode scripts
* Upper-case first letter
* At least two letters
* No leading or trailing whitespace
* Does not include the following characters: , , = , $ , " , ' , \
* Is in NFKC normalization form
* Does not contain the null character

Organisation (O) must represent a legal entity name - which is the beneficial owner of states on the ledger. For guidance on what exact legal entity name to write, see [here](https://corda.network/participation/legalentity.html)

Overall, the DN is one of the most common points of error in joining Corda Network, so take care to fill this out correctly. As part of standard onboarding checks for Corda Network, the Identity Operator may verify that these details have been accurately populated and reject requests where the population of these fields does not appear to be correct.

| | Mandatory | Length (chars) | Validation | Purpose |
| --- | --- | --- | --- | --- |
| **Organisation (O)** | Y | 128 | As per above, and additionally: No double-spacing. May not contain the words &quot;node&quot; or &quot;server&quot;. | The O field for the legal entity defines the beneficial owner of states on the ledger. This should be set to the **legal name** of the organisation, as it appears on the official trade register within the jurisdiction in which the entity is registered. This is used to define the owning organisation of the node / certificate. |
| **Organisation Unit (OU)** | N | 64 | As per above | This field is generally used to denote sub-divisions or units of the organisation (legal entity). It may be used by node operators for internal purposes to separate nodes used for different purposes by the same legal entity. |
| **Locality (L)** | Y | 64 | As per above | The city or town in which the registered head-office of the legal entity is located. If the company operates from New York City but is registered in Wilmington, Delaware then please use Wilmington |
| **Country (C)** | Y | 2 | 2-digit ISO code | The country in which the registered head-office of the legal entity is located. |
| **State (S)** | N | 64 | As per above | If your country operates a State or Province system (e.g. USA and Canada) please add the State in which the registered head-office of the legal entity is located. Do not abbreviate. For example, &quot;CA&quot; is not a valid state name. &quot;California&quot; is correct. If the company operates from New York but is registered in Delaware, please use Delaware |
| **Common Name (CN)** | N | 64 | As per above | Available for use by the node operator for their own internal purposes. Often used for home website urls in www. |
