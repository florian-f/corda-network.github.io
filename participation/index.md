|Corda Network Foundation|[Document history]({{ site.github.repository_url }}/blame/master/{{page.path}})|

Joining Corda Network
=====================

An outline of steps to join the Network is listed below. 

This assumes that Participants wish to operate a node and already have access to at least one CorDapp which they wish to deploy, as well as other considerations listed. A more detailed step-by-step guide will soon be available.

New Joiner Process 
------------------

*18 Feb 2019: Please note, the team is working hard to streamline this process, to provide an improved user experience.*

**Step 1.** Obtain Corda software - either: 
* Open Source, through [github](https://github.com/corda) under an Apache 2 license. 
* Corda Enterprise, available via a [Corda representative](https://www.r3.com/corda-enterprise-download/).

There is further guidance available on Corda Docs for [getting set up on Corda](https://docs.corda.net/getting-set-up.html).

**Step 2.** Request the Trust Root from Identity Operator by mailing doorman@r3.com, which will be sent back as a network-root-truststore.jks file. In future, the Trust Root will be packaged in the software distribution.

**Step 3.** [Deploy the node](https://docs.corda.net/deploying-a-node.html) - where applicable, with help from a Corda 
representative. 

**Step 4.** [Configure the node](https://docs.corda.net/corda-configuration-file.html) – a node.conf file must be included in the root directory of every Corda node. 

Configuring the node includes: 

4.1. **Choosing an email address.** The email address should belong to a suitably authorised employee of the node operator organisation. The email address is retained by the Operator for the purposes of contact in relation to identity checks (for onboarding) and any administrative or technical issues (on an ongoing basis). It is not included in the certificate. 

4.2. **Choosing a Distinguished Name** 
All nodes on Corda Network must have a Distinguised Name (DN) in their [participation certificate](https://docs.corda.net/corda-network/index.html#identity-service).
* Follow the guidelines [here](https://corda.network/participation/distinguishedname.html) to pick the right DN, as part of the onboarding process.
* A DN will include a legal entity name for your node. For guidance on which legal entity name to pick for your node, see [here](https://corda.network/participation/legalentity.html).

**4.3. Specifying URLs For Initial Registration**
The settings below must be added to the node.conf at the end of the file:

```
networkServices {
doormanURL=“https://prod-doorman2-01.corda.network/ED5D077E-F970-428B-8091-F7FCBDA06F8C”
networkMapURL=“https://prod-netmap2-01.corda.network/ED5D077E-F970-428B-8091-F7FCBDA06F8C”
}
devMode = false

tlsCertCrlDistPoint : “http://crl.corda.network/nodetls.crl”
tlsCertCrlIssuer : “CN=Corda TLS CRL Authority,OU=Corda Network,O=R3 HoldCo LLC,L=New York,C=US”
```

**Step 5.** Run the initial registration. 

Once the node.conf file is configured, the following should be typed to the command line:

```
java -jar corda.jar --initial-registration
``` 

This will send a Certificate Signing Request (with the relevant name and email) to the Identity Service.

A message similar to the below will be printed to the console:

```
Legal Name: O=ABC LIMITED, L=New York, C=US
Email: john.smith@abc.com

Public Key: EC Public Key
            X: d14bc17e650f2a317cbcb95e554f1e26808ca80f67ab804bbc911ec16673abbd
            Y: 1978b02a8e693ecd534ceef835091c376cfc4e506decc69b91a872fc13ad1aeb

-----BEGIN CERTIFICATE REQUEST-----
MIIBLTCBywIBADBMMQswCQYDVQQGEwJVUzERMA8GA1UEBwwITmV3IFlvcmsxFjAU
BgNVBAoMDVIzIEhvbGRDbyBMTEMxEjAQBgNVBAsMCUM4MTUyOTE2NzBZMBMGByqG
SM49AgEGCCqGSM49AwEHA0IABNFLwX5lDyoxfLy5XlVPHiaAjKgPZ6uAS7yRHsFm
c6u9GXiwKo5pPs1TTO74NQkcN2z8TlBt7Mabkahy/BOtGuugHTAbBgkqhkiG9w0B
CQExDgwMYWRtaW5AcjMuY29tMBQGCCqGSM49BAMCBggqhkjOPQMBBwNHADBEAiBA
KLF4NLrleNZPKMoxBrr/80fE3kVbFnYtkB2h0JhX1gIgPcV0X0xZQug+njKCyKgf
DkNUdQJPqhkBBEpgVqyZmE8=
-----END CERTIFICATE REQUEST-----
Submitting certificate signing request to Corda certificate signing server.
Successfully submitted request to Corda certificate signing server, request ID: 6CBB63558B4B2D9C94F8C14AB713432F60AF692EB30F2E12E628B089C517F3CF.
Start polling server for certificate signing approval.
```

Important: the Request ID given in the above should be noted and kept safe for future reference. 

**Step 6.** Sign the [Terms of Use](https://corda.network/participation/terms-of-use.html) legal document

*Sponsored Model*
Business Network Operators need to ensure their participants have signed the Terms of Use before they can receive a participation certificate. The Terms of Use are available as a click-through agreement which will provide direct confirmation of acceptance to the Corda Network Operator. If BNOs prefer to organise acceptance themselves, then they must forward appropriate documentary evidence for each participant (either a signed hard copy with wet signature or a scan of such hard copy). You must specify the precise Distinguished Names in order to confirm that the correct entity has signed and an accurate certificate can be issued.

**Step 7.** Identity Checks.

Identity Operator does verification checks – upon receipt of a CSR, a number of identity-related checks will be conducted, before issuing a certificate. 

**Identity checks do not constitute formal Know Your Customer (KYC) or Enhanced Due Diligence (EDD) checks. Node operators 
and their users are responsible for carrying out appropriate due diligence on any participant in relation to transactions 
performed via Corda Network.**

Upon receipt of a CSR, the Identity Operator will conduct a number of identity-related checks before issuing a certificate:
1.	The DN accurately reflects a real-world legal entity, as registered with an appropriate trade register
2.	The node operator (participating entity) has signed the Corda Network Terms of Use
3.	The contact email address provided is valid
4.	The owner of the email address and an independent and suitably qualified person in the same organisation is aware of / approves the CSR


*Email contact*

The Corda Network Operator will contact the owner of the email address provided in the CSR and it is important that the owner of this email address is aware of and prepared to respond to contact from the Corda Network Operator in relation to the CSR submission, and that they are able to do so on a timely basis. Issuance of the certificate cannot proceed until contact has been made and so any delay will add to the elapsed time to issue the certificate and enable the node to join the network.
Communications will be sent from 'Corda Network Onboarding' (doorman@r3.com). The email owner should ensure that this address is whitelisted by their email provider. 


**Step 8.** Once identity checks have been completed, a signed node CA certificate will be released by the Operator to the 
node. A node in polling mode will automatically download and install the certificate in its local trust store. It will 
also automatically generate additional identity and TLS certificates from the node CA certificate, which are required 
for subsequent operation of the node. 

At this point, the node will terminate and will need to be restarted. Type "java -jar <corda jar file>" into the command 
line. Once restarted, the node will then proceed to download the network map and discover other nodes within Corda Network. By the end of this process, joiners will be a participant in Corda Network and Corda Network Foundation. 

*Confirming your implementation*

Installation and configuration of your Corda applications must be undertaken by the node operator. Instructions to install CorDapps can be found on https://docs.corda.net. Specifics on application usage or installation should be available from your CorDapp provider.

Business Network Operators should co-ordinate any post-install tests that may involve a small number of low value transactions on the business network to assure themselves of the correct setup of their node. Node operators should co-ordinate with their Business Network Operator in this regard. All node-initiated activity on the network from the point of connection is the responsibility of the node operator.

Participation fee 
------------------

Billing details will be gathered, for a participation fee invoice, during this process. This will depend on if they are part of the **indirect** or **direct model**.

For further questions on this process, please [contact us](../about/contact.html) - preferably on the [mailing list](https://groups.io/g/corda-network).
