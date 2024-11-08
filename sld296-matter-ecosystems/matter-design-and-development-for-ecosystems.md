# Matter Design & Development for Ecosystems

This page provides a quick introduction to Matter ecosystems, their goals and advantages, and a presentation of a few already available ecosystems and their main features and differences.

## Details

### Introduction to Matter Ecosystems

While the Matter specification defines how devices can interact and be controlled, it does not determine how users will interface with those devices and under what conditions. This is left to the applications themselves, which each ecosystem offers being different. These ecosystems may choose to control devices differently, expose features in different ways, or offer differentiating options that other ecosystems do not. That being said, a device that implements the Matter specification will still operate properly within any Matter-based ecosystem.

### Reasons to Support Ecosystems Directly

- Testing interoperability (critical for every Matter device maker)
  - Specification implementation doesn't always guarantee smooth operation.
  - Application implementations of Matter may be different. To ensure a quality customer experience, device makers should test with the primary interfaces to their users which will be the ecosystems.
- Ease of development
  - Setting up an ecosystem hub is more straightforward than creating a Raspberry Pi Matter controller.
  - Significant time can be spent on setting up the OpenThread Border Router (OTBR), taking time away from developing your end device.
  - Some ecosystems provide great tools and programs to learn, develop, test, launch, and maintain devices.
- Differentiation (device makers who want to create best-in-class products)
  - Ecosystem providers want to use their specific strengths to offer advantages within their ecosystems, providing a superior user experience.
- Marketing / badging (most device makers will benefit)
  - Ecosystem-specific certification will generally come with a branding badge to use on their product, clearly signaling to consumers that the product works with a given ecosystem.
  - We anticipate badging to be a critical part of IoT adoption, being less important when IoT is ubiquitous and things "just work".
  - Currently, it is a good idea to have a product clearly state which ecosystem they are guaranteed to be compatible with.

### Ecosystem Comparison

:::custom-table{width=16%,14%,14%,14%,14%,14%}
|              | >           |Matter / Thread| >           | Matter / WiFi |                    |
| ------------- | ----------| :----------- | --------- | :----------- | ------------------- |
| **Ecosystem** | :custom-cell[**Devices**]{style=align-left} | :custom-cell[**Launched?**]{style=align-left} | :custom-cell[**Devices**]{style=align-left} | :custom-cell[**Launched?**]{style=align-left} | **Other protocols** |
| **Amazon** | :custom-cell[:list[Echo Gen 4]]{style=align-left} | No, targeting launch in Q1 | :custom-cell[:list[Echo Gen 4\nEcho devices: Echo Dot 5th gen, Echo Studio, Echo Show 8, etc.]]{style=align-left} | Yes (on Android only) | Zigbee, BT Mesh, Sidewalk |
| **Apple** | :custom-cell[:list[HomePod Mini\nApple TV 4K]]{style=align-left} | Yes (iOS/tvOS 16.1+) | :custom-cell[:list[HomePod Mini\nApple TV 4K]]{style=align-left} | Yes (iOS/tvOS 16.1+) | HomeKit over WiFi/BLE |
| **Google** | :custom-cell[:list[Nest Hub 2nd gen\nNest Hub Max\nNext WiFi]]{style=align-left} | Yes (on Android only, iOS support coming later) | :list[Google Mini\nNest Mini\nNest Hub 1st gen\nNest Hub 2nd gen\nNest Hub Max\nNest WiFi\nNest Audio] | Yes (on Android only, iOS support coming later) | No  |
| **Samsung SmartThings** | :custom-cell[:list[Aeotec SmartThings Hub\nHub Everywhere (Samsung branded TVs, charging hubs, refrigerators)]]{style=align-left} | Yes (on Android only, iOS support coming later) | :custom-cell[:list[Aeotec SmartThings Hub\nHub Everywhere (Samsung branded TVs, charging hubs, refrigerators)]]{style=align-left} | Yes (on Android only, iOS support coming later) | Zigbee, Z-Wave |
:::

### Ecosystem Status for Developers

#### Amazon ([link](https://developer.amazon.com/en-US/docs/alexa/smarthome/matter-support.html#get-started-with-matter))

- Development experience: There is no well-defined early access program yet.
- Certification programs: Amazon plans to have a badging and certification program for Matter devices similar to their current Works with Alexa program for Zigbee devices. This is expected to be available sometime in the first half of 2023.
- Differentiating features: Amazon has announced Matter Simple Setup for Matter devices which will be a part of their Frustration Free Setup infrastructure for smart home products. This will have its own certification program and badging/marketing materials.

#### Google ([link](https://developer.apple.com/apple-home/matter/))

- Development experience: A comprehensive set of online tools, integrations, and documents are provided to help decrease the workload for a developer to create a new Matter product. The Google Home Developer Center and Developer Console assist developers in building Matter devices. A developer can build, test, certify, launch, and update their Matter product using Google’s online platforms.
- Certification programs: Google has created a Works With Google Home (WWGH) certification program for Matter devices that will be run entirely through the Google Home Developer Console. Developers will then have access to WWGH badging and marketing materials.
- Differentiating features: Additional Intelligence Clusters are available for those who wish to implement them. These give a whole home context to the implementing device. An example of this is the Home and Away feature, which allows a device to act based on knowledge of the homeowner’s presence.

#### Samsung SmartThings ([link](https://developer.samsung.com/smartthings))

- Development experience: Samsung SmartThings has been operating an Early Access Program for a limited set of partners for early access to new feature development on their SmartThings Android app and hub firmware. More details are expected to be available in the first half of 2023.
- Certification programs: A Works with SmartThings certification program is expected but the details are currently unknown.
