# Silicon Labs Wi-SUN SoC Border Router

![](resources/image2.PNG)The Wi-SUN SoC Border Router demonstration provides a Wi-SUN Border Router implementation running entirely on the EFR32. It provides an easy and quick means to evaluate the Silicon Labs Wi-SUN stack solution without deploying an expensive and cumbersome production-grade Wi-SUN Border Router. A CLI (Command-Line Interface) is exposed to facilitate the configuration.

## Getting Started With the Solution

The Wi-SUN SoC Border Router sample creates a Wi-SUN network that the other Wi-SUN nodes can join.

To get started with the demonstration, follow these steps:

1. In the Debug Adapters view, select the device to be used as the Border Router.

2. Navigate to the **EXAMPLE PROJECTS & DEMOS** tab and turn off the Example Projects filter.

3. Click **RUN** next to the **Wi-SUN – SoC Border Router** project.

4. ![](resources/image3.png)In the Debug Adapter view, right click your chosen device, and click on **Launch Console**.

5. Start the Border Router using the following command:

```C
> wisun start
```

## Wi-SUN - SoC Border Router Solution Limitations :

The Wi-SUN Border Router demonstration is delivered only in a binary format. The implementation does not scale for a production-grade Border Router maintaining several thousand Wi-SUN nodes.

The Wi-SUN Border Router demonstration is required to use the other Wi-SUN sample applications. The Wi-SUN Border Router creates a Wi-SUN network that the Wi-SUN nodes can join. When part of the same network, the Wi-SUN nodes can exchange IP packets.
