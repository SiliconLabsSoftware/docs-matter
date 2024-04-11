# Matter Repositories, Commit Hashes, Versioning, and Maintenance

## Repositories

The following repositories, branches and commit hashes are to be used together in this release of the Silicon Labs Matter Out of Box Experience.

### Open Thread Border Router (OTBR)

| Repo                                       | Branch | Commit Hash                              |
| ------------------------------------------ | ------ | ---------------------------------------- |
| https://github.com/SiliconLabs/ot-br-posix | main   | 42f98b27b |

### Radio Co-Processor (RCP)

| Repo                                    | Branch | Commit Hash                              |
| --------------------------------------- | ------ | ---------------------------------------- |
| https://github.com/SiliconLabs/ot-efr32 | main   | e75c76737 |

### Matter chip-tool

| Repo                                            | Branch | Commit Hash                              |
| ----------------------------------------------- | ------ | ---------------------------------------- |
| https://github.com/openthread/openthread | main  | 7074a43e4 |

### Connectivity Standards Alliance (CSA) connectedhomeip (Matter)

| Repo                                            | Branch | Commit Hash                              |
| ----------------------------------------------- | ------ | ---------------------------------------- |
| https://github.com/project-chip/connectedhomeip | master | d140d5c8775 |


## Versioning Scheme

**Matter GSDK extension and Silabs Matter Github (SMG) are separate products. They use the same versioning scheme, but there is no relationship between these two versions.**

- **FORMAT: vMAJOR.MINOR.PATCH-CSA\_VERSION-PRE\_RELEASE**

- Silicon Labs versions e.g., 3.0.0

- CSA Matter version e.g., 1.1

- [Optional] Prerelease flag e.g., alpha.1

**Example:** v3.0.0-1.1-alpha.1

Update digits based on the following criteria:

- **Major**

  - CSA ups the major version number, or

  - Major GSDK version supported, or

  - Miscellaneous breaking change

- **Minor**

  - CSA ups the minor version number, or

  - Minor GSDK version supported, or

  - Silabs updates e.g., new sample app, documentation, bug fixes, or

  - Silabs hardware platform added, or

- **Patch**

  - Patch GSDK version supported, or

  - Targeted bug fixes

- **Pre-Release**

  - As needed, e.g. release after TE1 can be called v2.3.0-1.2-alpha.1

## Maintenance Releases

## Matter GSDK Extension

| **Release** | **Date** | **GSDK** | **WiSeConnect 3 SDK** | **Status** |
|-------------|----------|----------|----------|----------|
| v1.0.1-1.0 | 19-Dec-22  | 4.2.0 |  N/A | Obsolete | 
| v1.0.3-1.0 | 3-Feb-23   | 4.2.1 |  N/A | Obsolete |
| v1.0.4-1.0 | 16-Feb-23  | 4.2.1 |  N/A | Obsolete |
| v1.0.5-1.0 | 10-Mar-23  | v4.2.2, v4.2.3, v4.2.4, v4.2.5 | N/A | Monitored |
| v2.0.0-1.1 | 8-June-23  | v4.3.0 | N/A | Maintained |
| v2.1.0-1.1 | 27-July-23 | v4.3.1 | v3.0.10 | Obsolete |
| v2.1.1-1.1 | 9-Oct-23 | v4.3.2, v4.3.3 | v3.1.0 | Maintained |
| v2.2.0-1.2 | 13-Dec-23 | v4.4.0, v4.4.1 | v3.1.1 | Obsolete |
| v2.2.1-1.2 | 10-Apr-24 | v4.4.1, v4.4.2 | v3.1.4 | Active |


## Silabs Matter Github (SMG)

| **Release** | **Date** | **GSDK** | **WiSeConnect 3 SDK** | **Status** |
|-------------|----------|----------|----------|
| v0.1.0 | 26-July-22 | v4.1.0 | N/A | Obsolete |
| v0.2.0 | 17-Aug-22  | v4.1.0 | N/A | Obsolete |
| v0.3.0 | 8-Sept-22  | v4.1.1 | N/A | Obsolete |
| v0.4.0 | 13-Oct-22  | v4.1.1 | N/A | Obsolete |
| v1.0.0 | 2-Nov-22   | v4.1.1 | N/A | Obsolete |
| v1.0.2-1.0 | 19-Dec-22 | v4.1.1 | N/A | Monitored |
| v1.1.0-1.1 | 24-Feb-23 | v4.2.0 | N/A | Monitored |
| v2.0.0-1.1 | 18-May-23 | v4.2.0 | N/A | Obsolete |
| v2.1.0-1.1 | 23-June-23 | v4.2.3 | N/A | Maintained |
| v2.2.0-1.2-alpha-1 | 30-Aug-23 | v4.3.1 | v3.0.10  | Obsolete |
| v2.2.0-1.2 | 25-Oct-23 | v4.3.2 | v3.1.0  | Active |