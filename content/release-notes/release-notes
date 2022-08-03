---
uid: ReleaseNotes
---

# Release Notes

PI Web API 2021 SP3 
1.17.0.200

## Overview

The PI Web API is a RESTful service in the Developer Technologies suite, designed to provide cross-platform web and mobile programmatic interfaces to the PI System. The PI Web API presently contains basic functionality needed to retrieve and manipulate time series data from the PI Data Archive, Asset and Event Frame data from the PI Asset Framework, and to index and search on objects within the PI System.

The PI Web API belongs to the OSIsoft Developer Technologies family of products, which is designed to support the implementation of custom applications on top of the PI System, as well as the integration of PI System data with other applications and business systems such as Microsoft Office or SQL Server, Enterprise Resource Planning systems (ERPs), reporting and analytics platforms, web portals, geospatial and maintenance systems. The Developer Technologies cover a wide range of use cases in various environments, programming languages, operating systems, and infrastructures.

## Enhancements

PI Web API 2021 SP3 introduces the following enhancements:

- Add support for simplified OMF DELETE messages.
- Make PI Web API to handle OMF messages case insensitively
- Process OMF CONTAINER Requests Using Non-Destructive Writes to DA
- Add new PI Point query capabilities

## Fixes

This section lists items that were resolved or added in this release of PI Web API.

| Work Item | Description                                                                     |
| :-------- | :------------------------------------------------------------------------------ |
| 320517    | Retrieving child Event Frames when path is ambiguous returns the wrong children |
| 287966    | `InitializeSystemTimeZoneCache()` throws duplicated ID exception                |

## Known Issues

This section lists problems and enhancements that have been deferred until a future release.

| Work Item | Description                                                                                                                                                                                                                                                                                                                                                                                              |
| :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 61413     | Change in PI Mappings do not cause reindexing of affected PI Points.                                                                                                                                                                                                                                                                                                                                     |
| 61475     | PI Web API silent installation fails if InstallationConfig.json path has spaces.                                                                                                                                                                                                                                                                                                                         |
| 63862     | PI Web API Admin Utility adds CA-signed certificate to local machine Trusted People store.                                                                                                                                                                                                                                                                                                               |
| 64081     | The OMF feature will not be available after modifying an installation using the control panel and will return 404 not found error. To work around the issue, run the PI Web API Admin Utility after the installation.                                                                                                                                                                                    |
| 64268     | If a user is removed from the "PI Web API Admins" group and later runs the installer, that user will not be re-added to the group. As a workaround, the user can be manually added to the "PI Web API Admins" group.                                                                                                                                                                                     |
| 64558	    | Streams controller serves stale data for static attribute values when the Cache-Control: no-cache header is specified.                                                                                                                                                                                                                                                                                   |
| 82298     | Indexed search source is marked as needing repair if the primary source is removed from collective.                                                                                                                                                                                                                                                                                                      |
| 106102    | Incremental indexed search crawls remove relative paths.                                                                                                                                                                                                                                                                                                                                                 |
| 112175    | If several hundred PI Mappings exist for a single PI System, the Indexed Search service may not be able to calculate the correct access controls. A straightforward workaround is to map to an Active Directory group rather than to individual accounts.                                                                                                                                                |
| 129068    | PI Web API doesn't return all allowed methods in WWW-Authenticate challenge, e.g. "Bearer".                                                                                                                                                                                                                                                                                                              |
| 130566    | Non-ASCII characters cannot be used in usernames or passwords in Basic Authentication.                                                                                                                                                                                                                                                                                                                   |
| 137943    | PI Crawler reports an identity mismatch error if an ANAME record is defined.                                                                                                                                                                                                                                                                                                                             |
| 145108    | Indexed Search Crawler does not acknowledge AF Attribute category name change until a different change is made to the attribute.                                                                                                                                                                                                                                                                         |
| 150407    | Providing duplicated Web Ids in StreamSet controller's adhoc actions will cause 404 error.                                                                                                                                                                                                                                                                                                               |
| 179690    | Incorrect log message of crawler version change when security mappings are modified.                                                                                                                                                                                                                                                                                                                     |
| 189985    | Stream Updates Status field does not account for Errors.                                                                                                                                                                                                                                                                                                                                                 |
| 192785    | Retrieving Digital State values may fail if the Digital Set has been changed.                                                                                                                                                                                                                                                                                                                            |
| 211321    | Large numbers of security descriptors in Indexed Search can result in the error "maxClauseCount is set to 1024".                                                                                                                                                                                                                                                                                         |
| 256431    | Changing the EventLogDebugAnalyticCharacterLimit app.config setting stops OMF request/responses from being logged.                                                                                                                                                                                                                                                                                       |
| 258584    | PI Web API incorrectly converts string stream values that are formatted as valid ISO8601 timestamps to DateTime format.                                                                                                                                                                                                                                                                                  |
| 268437    | OMF Property that is marked as both 'IsIndex' or 'IsName' and 'IsQuality' breaks type.                                                                                                                                                                                                                                                                                                                   |
| 269726    | Indexed Search Admin page graph is incompatible with IE11                                                                                                                                                                                                                                                                                                                                                |
| 276901    | OMF DATA of type 'number' doesn't emit loss of precision warnings                                                                                                                                                                                                                                                                                                                                        |
| N/A       | Security settings of 'Basic' or 'Anonymous' prevent crawler execution. There is a known issue with any security setting other than 'Kerberos' creating problems with the PI Web API Indexed Search crawler from executing. Workaround is to use 'Kerberos' security settings. No work item is assigned to address this issue.                                                                            |
| N/A       | In a Remote Desktop Session to a Windows Server 2016 machine, the PI Web API Admin Utility can become unresponsive upon enumerating available SSL certificates. As a workaround, cause the Remote Desktop Session to lose focus (such as clicking outside the Remote Desktop Connection window), and then restore focus to the PI Web API Admin Utility. No work item is assigned to address this issue. |

## System Requirements

### Operating Systems

The preferred, supported deployment platforms are Windows Server 2022, Windows Server 2019, Windows Server 2016 or Windows Server 2012 R2.

Windows Server 2012 (Full Desktop Installation only) may also be used; however, use of Windows Server 2012 is discouraged, as planned enhancements to PI Web API will require functionality that is only available in later versions of Windows.

Microsoft's client operating systems, Windows 11 (64-bit only) may be used in a limited capacity for development and testing purposes only. Please make sure that two entries "RegisteredOwner" and "RegisteredOrganization" exist under the Registry Key `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion`. If
not, add those two entries with empty string values.

Earlier versions of Windows and non-x64 versions of Windows are not supported.

### Server Platforms

Core:

- PI Data Archive 2018 SP3 Patch 3 (3.4.440.477) or later is recommended.
- PI AF Server 2018 SP3 Patch 3 (2.10.9.593) is recommended.

OMF:

- PI Data Archive 2018 SP3 Patch 3 (3.4.440.477) or later is recommended.
- PI AF Server 2018 SP3 Patch 3 (2.10.9.593) is recommended.

Not all features, bug fixes, and performance enhancements may be available with older PI Data Archive or PI AF Servers.

## Distribution Kit Files

The installer is released as a self-extracting distribution kit that contains:

- Installation files for .NET Framework 4.8.
- Installation files for PI AF Client 2018 SP3 Patch 3 (x64), which includes the
  AF Client installer, and installers for its prerequisites:
  - Microsoft Visual C++ 2019 Redistributable (x86 and x64)
  - PI Network Subsystem 3.4.435.538
  - PI Buffer Subsystem 4.9.0.37
- The PI Web API Windows Installer Database (MSI) file that is signed by OSIsoft

### Installation and Upgrade

#### Before You Install

1. Verify that the system you plan to use is running a supported operating
   system.
2. Verify that you can run the installer as an Administrator.

#### Installation and Upgrades

The PI Web API installer has a graphical user interface, which allows you to
perform an installation or upgrade of PI Web API. At the end of an installation
or upgrade, the PI Web API Admin Utility is automatically launched. Go through
all the steps in the PI Web API Admin Utility to complete the installation or
upgrade. Detailed information and a walk-through of installation is available in
the _PI Web API User Guide_.

The PI Web API installer supports silent installations. Please refer to the _PI
Web API User Guide_ for detailed information.

### Uninstalling PI Web API

Remove the product using **Uninstall a program** in the Windows Control Panel,
or alternatively, re-run the Installation Kit and follow the prompts to remove
the product.

Uninstalling the product will not remove:

- Any SSL certificates that were created during the installation process
- The binding of the selected SSL certificate to the port used by PI Web API in
  the Windows HTTP service's configuration
- The URL reservation for PI Web API in the Windows Kernel routing table
- The locally stored indexes for Indexed Search functionality

The above items may be removed manually if desired.

## Security Information and Guidance

### OSIsoft's Commitment

Because the PI System often serves as a barrier protecting control system
networks and mission-critical infrastructure assets, OSIsoft is committed to (1)
delivering a high-quality product and (2) communicating clearly what security
issues have been addressed. This release of PI Web API is the highest-quality
and most secure version of the PI Web API released to date. OSIsoft's commitment
to improving the PI System is ongoing, and each future version should raise the
quality and security bar even further.

### Vulnerability Communication

The practice of publicly disclosing internally discovered vulnerabilities is
consistent with the [Common Industrial Control System Vulnerability Disclosure
Framework](https://us-cert.cisa.gov/sites/default/files/ICSJWG-Archive/ICSJWG_Vulnerability_Disclosure_Framework_Final_1.pdf)
developed by the [Industrial Control Systems Joint Working Group
(ICSJWG)](https://us-cert.cisa.gov/ics/Industrial-Control-Systems-Joint-Working-Group-ICSJWG).
Despite the increased risk posed by greater transparency, OSIsoft is sharing
this information to help you make an informed decision about when to upgrade to
ensure your PI System has the best available protection.

For more information, refer to OSIsoft's Ethical Disclosure policy:
[https://www.osisoft.com/terms-and-conditions/ethical-disclosure](https://www.osisoft.com/terms-and-conditions/ethical-disclosure)

To report a security vulnerability, refer to:
[https://www.osisoft.com/terms-and-conditions/report-security](https://www.osisoft.com/terms-and-conditions/report-security)

### Vulnerability Scoring

OSIsoft has selected the [Common Vulnerability Scoring System
(CVSS)](https://www.first.org/cvss/v2/guide) to quantify the severity of
security vulnerabilities for disclosure. To calculate the CVSS scores, OSIsoft
uses the [National Vulnerability Database (NVD)
calculator](https://nvd.nist.gov/vuln-metrics/cvss/v2-calculator?calculator&version=2)
maintained by the National Institute of Standards and Technology (NIST). OSIsoft
uses Critical, High, Medium and Low categories to aggregate the CVSS Base scores. This
removes some of the opinion related errors of CVSS scoring. As noted in the
[CVSS specification](https://www.first.org/cvss/specification-document), Base
scores range from 0 for the lowest severity to 10 for the highest severity.

### Overview of New Vulnerabilities Found or Fixed

This section is intended to provide relevant security-related information to guide 
your installation or upgrade decision. OSIsoft is proactively disclosing aggregate 
information about the number and severity of PI Web API security 
vulnerabilities that are fixed in this release.

For this release of PI Web API, four security vulnerabilities have been
identified and fixed. The table below provides an overview of the types and
severity of the security fixes.

Security Vulnerabilities fixed in this release

| Severity Category | CVSS Base Score Range | Number of Fixed Vulnerabilities |
| :---------------- | :-------------------- | :------------------------------ |
| Critical          | 9 – 10                | 0                               |
| High              | 7.0 – 8.9             | 0                               |
| Medium            | 4.0 – 6.9             | 0                               |
| Low               | 0 – 3.9               | 0                               |

#### Vulnerability Mitigations in PI Web API v1.17.0 Release

The following vulnerabilities were identifed in PI Web API v1.17.0 Release.

| Component         | Version | CVE or Reference                | CVSS | Mitigation                                                                                                                                                                                                                                                                                               |
| :---------------- | :------ | :------------------------------ | :--- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RazorEngine       | 3.10.0  | CVE-2021-46703                  | 9.8  | The PI Web API does not use the IsolatedRazorEngineService or allow users to externally control the contents of Razor templates.                                                                                                                                                                         |
| jquery-validation | 1.19.3  | CVE-2022-31147                  | 7.5  | Indexed Search and PI Web API do not use the url2() method.                                                                                                                                                                                                                                              |
| jquery-validation | 1.19.3  | CVE-2021-43306 (BDSA-2022-1590) | 7.5  | Indexed Search and PI Web API do not use the url2() method.                                                                                                                                                                                                                                              |
| jquery-validation | 1.19.3  | BDSA-2022-1898                  | 6.7  | Indexed Search and PI Web API do not use the url2() method.                                                                                                                                                                                                                                              |
| jQuery            | 3.6.0   | BDSA-2021-3651                  | 4.9  | The link to the blindsignals web site is included in jQuery 3.6.0 source. The link is not surfaced to any web user interface. Utilizing this link requires accessing the source and copying the link into a browser. A newer version of jQuery without this vulnerability is not available at this time. |

#### Vulnerability Mitigations in PI Buffer Subsystem 2018 SP2 Patch 2 and PI Network Subsystem Support (PINS)

The following vulnerabilities were identified in PI Buffer Subsystem 2018 SP2 Patch 2 and PI Network Subsystem Support (PINS) and mitigated. PI Buffer Subsystem 2018 SP2 Patch 2 and PI Network Subsystem Support (PINS) are deployed with PI Web API 1.7.0.

| Component | Version | CVE or Reference | CVSS | Mitigation                                                                                                                                                                                      |
| :-------- | :------ | :--------------- | :--- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SQLite    | 3.31.1  | CVE-2020-11656   | 9.8  | Use of SQLite is through compiled static statements. ALTER TABLE is not used.                                                                                                                   |
| SQLite    | 3.31.1  | CVE-2020-11655   | 7.5  | Use of SQLite is through compile static statements. Windows aggregate methods are not used.                                                                                                     |
| SQLite    | 3.31.1  | CVE-2020-13630   | 7    | Use of SQLite is through compile static statements. The snippet feature is not used.                                                                                                            |
| SQLite    | 3.31.1  | BDSA-2021-2585   | 6.7  | The SQLite Expert extension that was reported as vulnerable is not used. It is not included as part of the source distribution that OSIsoft (now AVEVA) uses, as it is an experimental feature. |
| SQLite    | 3.31.1  | BDSA-2020-1330   | 6.7  | Use of SQLite is through compiled static statements. This issue requires Window select methods to execute aggregate functions, which the compiled statements do not use.                        |
| SQLite    | 3.31.1  | BDSA-2020-0327   | 6.7  | Use of SQLite is through compiled static statements.                                                                                                                                            |
| SQLite    | 3.31.1  | CVE-2020-13434   | 5.5  | Use of SQLite is through compiled static statements. No printf statements are used.                                                                                                             |
| SQLite    | 3.31.1  | CVE-2020-13632   | 5.5  | Use of SQLite is through compiled static statements.                                                                                                                                            |
| SQLite    | 3.31.1  | CVE-2020-13631   | 5.5  | Use of SQLite is through compiled static statements. There is no path for arbitrary SQL statements to get executed.                                                                             |
| SQLite    | 3.31.1  | CVE-2020-13435   | 5.5  | Use of SQLite is through compiled static statements. No aggregate window functions are used.                                                                                                    |
| SQLite    | 3.31.1  | CVE-2020-15358   | 5.5  | Use of SQLite is through compiled static statements. We don't use constants in SELECT queries.                                                                                                  |

#### Vulnerability Mitigations in PI AF Client 2018 SP3 Patch 3

This vulnerability was identified in PI AF Client 2018 SP3 Patch 3 and mitigated. PI AF Client 2018 SP3 Patch 3 is deployed with PI Web API v1.17.0.

| Component       | Version | CVE or Reference | CVSS | Mitigation                                                                                           |
| :-------------- | :------ | :--------------- | :--- | :--------------------------------------------------------------------------------------------------- |
| Newtonsoft.Json | 11.0.1  | BDSA-2018-5195   | 6.7  | No code paths result in JSON parsing and subsequent serialization resulting in the DoS vulnerability |

## Documentation Overview

These release notes comprise a part of the following documentation set that
supports PI Web API:

**PI Web API 2021 SP3 Programmer Reference**: This reference is included in the
product. It is an online API reference meant for developers who wish to program
against the services provided in the product. It is accessible as HTML from the
link `https://servername/piwebapi/help`, where `servername` is the hostname of
the server on which this product has been installed.

**PI Web API 2021 SP3 User Guide**: This user guide provides information relevant to
the configuration, settings, and administration of the product, and contains
steps and helpful information for resolving problems with the product.

**PI Square and PI Developers Club**: The OSIsoft [PI
Square](https://pisquare.osisoft.com/) Community website has free resources to
help you with the programming and integration of OSIsoft products. Additional
benefits are available on a paid subscription basis to members of [PI Developers
Club](https://pisquare.osisoft.com/community/developers-club).

Additional information about the PI Developer Platform, PI Data Archive, PI
Asset Framework, and other topics of interest can be found in respective books
available on the [OSIsoft Technical Support and Resources Web
site](https://my.osisoft.com/).

## Technical Support and Resources

For technical assistance, contact OSIsoft Technical Support at +1 510-297-5828
or log a case through the OSIsoft Customer Portal. Additionally, the Contact Us
page on the portal offers contact options for customers outside of the United
States. This software and related content are available from the Product section
of the OSIsoft customer portal at
[https://my.osisoft.com](https://my.osisoft.com).

When you contact OSIsoft Technical Support, be prepared to provide this
information:

- Product name, version, and build numbers
- Computer platform (CPU type, operating system, and version number)
- Time that the difficulty started
- Log files at that time
- Details of any environment changes prior to the start of the issue
- Summary of the issue, including any relevant log files during the time the
  issue occurred

The [PI Square](https://pisquare.osisoft.com/) community has resources to help
you with your technical questions. [PI Developers
Club](https://pisquare.osisoft.com/community/developers-club) program offers
specific services to developers and system integrators.
