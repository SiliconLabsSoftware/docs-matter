# Matter Versioning and Release Maintenance

**Silicon Labs Matter GitHub is being phased out in favor of using the Matter GSDK Extension that is available thru Studio and standalone via SLC-CLI.**

## Versioning Scheme

- **FORMAT: vMAJOR.MINOR.PATCH\_VERSION-PRE\_RELEASE**

- Silicon Labs versions e.g., 3.0.0

- Connectivity Standards Aliiance Matter version e.g., 1.1

- [Optional] Prerelease flag e.g., alpha.1

**Example:** v3.0.0-1.1-alpha.1

Update digits based on the following criteria:

- **Major**

  - Connectivity Standards Alliance ups the major version number, or

  - Major GSDK version supported, or

  - Miscellaneous breaking change

- **Minor**

  - Connectivity Standards Alliance ups the minor version number, or

  - Minor GSDK version supported, or

  - Silabs updates e.g., new sample app, documentation, bug fixes, or

  - Silabs hardware platform added, or

- **Patch**

  - Patch GSDK version supported, or

  - Targeted bug fixes

- **Pre-Release**

  - As needed, e.g. release after TE1 can be called v2.3.0-1.2-alpha.1

    - To identify targeted feature requests/SQA quality level testing

      - alpha level quality to identify non-standard SQA level testing

      - beta level quality to identify certain SQA testing, but still in early development


## Release Maintenance

### Matter GSDK Extension

| **Release** | **Date** | **GSDK** | **WiSeConnect 3 SDK** | **Status** |
|-------------|----------|----------|----------|----------|
| v1.0.1-1.0 | 19-Dec-22  | v4.2.0 |  N/A | Obsolete | 
| v1.0.3-1.0 | 3-Feb-23   | v4.2.1 |  N/A | Obsolete |
| v1.0.4-1.0 | 16-Feb-23  | v4.2.1 |  N/A | Obsolete |
| v1.0.5-1.0 | 10-Mar-23  | v4.2.2, v4.2.3, v4.2.4, v4.2.5 | N/A | Monitored |
| v2.0.0-1.1 | 8-June-23  | v4.3.0 | N/A | Obsolete |
| v2.1.0-1.1 | 27-July-23 | v4.3.1 | v3.0.10 | Obsolete |
| v2.1.1-1.1 | 9-Oct-23   | v4.3.2, v4.3.3 | v3.1.0 | Maintained |
| v2.2.0-1.2 | 13-Dec-23  | v4.4.0, v4.4.1 | v3.1.1 | Obsolete |
| v2.2.1-1.2 | 10-Apr-24  | v4.4.1, v4.4.2 | v3.1.4 | Active |

