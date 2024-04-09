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


### Connectivity Standards Alliance (CSA) connectedhomeip (Matter)

| Repo                                            | Branch | Commit Hash                              |
| ----------------------------------------------- | ------ | ---------------------------------------- |
| https://github.com/project-chip/connectedhomeip | v1.1-branch | 8f66f4215bc0708efc8cc73bda80620e67d8955f |

### Matter chip-tool

| Repo                                            | Branch | Commit Hash                              |
| ----------------------------------------------- | ------ | ---------------------------------------- |
| https://github.com/openthread/openthread | main  | 7074a43e4 |


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

| **Release** | **Date** | **GSDK** | **Status** |
|-------------|----------|----------|----------|
| v1.0.1-1.0 | 19-Dec-22 | 4.2.0 | Obsolete |
| v1.0.3-1.0 | 3-Feb-23 | 4.2.1 | Obsolete |
| v1.0.4-1.0 | 16-Feb-23 | 4.2.1 | Obsolete |
| v1.0.5-1.0 | 10-Mar-23 | :para [4.2.2] :para[4.2.3] | Maintained |
| v2.0.0-1.1 | 8-June-23 | 4.3.0 | Obsolete |
| v2.1.0-1.1 | 27-July-23 | 4.3.1 | Active |
| v2.1.1-1.1 | :para[4-Oct-23] :para[GSDK 4.3.2] :para[(917 Pre-Cert)] | 4.3.2 | |
| :para[v2.1.2-1.1] :para[Tentative] | :para [31-Oct-23] :para[(917 GA)] | 4.3.2 | |
| v2.2.0-1.2 | 6-Dec-23 | 4.4.0 | |
| v2.2.1-1.2 | 10-Apr-23 | 4.4.2 | |

## Silabs Matter Github (SMG)

| **Release** | **Date** | **GSDK** | **Status** |
|-------------|----------|----------|----------|
| v0.1.0 | 26-July-22 | 4.1.0 | Obsolete |
| v0.2.0 | 17-Aug-22 | 4.1.0 | Obsolete |
| v0.3.0 | 8-Sept-22 | 4.1.1 | Obsolete |
| v0.4.0 | 13-Oct-22 | 4.1.1 | Obsolete |
| v1.0.0 | 2-Nov-22 | 4.1.1 | Obsolete |
| v1.0.2-1.0 | 19-Dec-22 | 4.1.1 | Maintained |
| v1.1.0-1.1 | 24-Feb-23 | 4.2.0 | Obsolete |
| v2.0.0-1.1 | 18-May-23 | 4.2.0 | Obsolete |
| v2.1.0-1.1 | 23-June-23 | 4.2.3 | Active |
| v2.2.0-1.2-alpha-1 | 30-Aug-23 | 4.3.1 | |
| v2.2.0-1.2 | Oct | 4.3.2 | |
