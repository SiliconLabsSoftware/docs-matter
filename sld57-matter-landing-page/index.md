# Silicon Labs Matter

The Matter protocol leverages existing IP technologies, including Wi-Fi and Thread, to build a unified wireless connectivity ecosystem for smart homes. Internet Protocol (IP)-based networking provides manufacturers with simplified development while improving device compatibility for consumers.

Silicon Labs supports Matter on both 802.15.4 (Thread) and 802.11 (Wi-Fi) transport protocols. The Thread development use case differs from Wi-Fi because the Thread protocol requires an OpenThread Border Router (OTBR).

The Unify Matter Bridge is an application that makes legacy devices, such as
Z-Wave and Zigbee devices, accessible on a Matter fabric. It does so by acting as
an _IoT Service_ in a Unify Framework.

![Silicon Labs Matter Summary](./resources/silicon-labs-matter.png)

## Two Paths for Development

These pages are for users who want to develop Matter applications in Simplicity Studio. The Simplicity Studio development path is the preferred path if you are looking for a GUI-based development experience in which you can create production-ready projects from a well-tested library. The Simplicity Studio development path also natively supports development on the Windows operating system. As a result, Windows users should use Simplicity Studio for their development environment.

Alternatively you can develop applications directly out of the [Silicon Labs Matter GitHub repo](https://github.com/SiliconLabs/matter). Complete documentation for the GitHub development use case is provided in the [Silicon Labs Matter GitHub Documentation](https://github.com/SiliconLabs/matter/blob/latest/docs/silabs/README.md). This path is best for those who are experienced working with Matter and Silicon Labs products, prefer working with GitHub and a workflow that's not IDE-driven, or need access to newer features sooner at the cost of lesser test coverage.

## Other Resources

**To see release notes** containing list of features and knowns issues go to [Matter Release Notes on Silicon Labs Matter Extension](https://github.com/SiliconLabs/matter_extension/releases/tag/v2.1.0). 

**If you are new to Matter** or would like more information about Silicon Labs Matter-based products, see the [Matter content on silabs.com](https://www.silabs.com/wireless/matter).

**For background information on the Matter standard**, see the [Connectivity Standard Alliance page](https://csa-iot.org/all-solutions/matter/).

**To quickly make a simple Matter network**, see the [quick-start guides](/matter/<docspace-docleaf-version>/matter-overview).

**To develop your own customized applications** with Matter over Thread and Matter over Wi-Fi, see the [Matter Developer's Guide](/matter/<docspace-docleaf-version>/matter-developers-guide-overview).
