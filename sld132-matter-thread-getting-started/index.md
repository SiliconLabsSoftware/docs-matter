# Matter over Thread Quick-Start Guide

These pages describe how to create a simple Matter network in which you can use a switch to control a light, described in more detail below under [A Typical Setup](#a-typical-setup).

You should have obtained hardware and installed software as described in the [Quick-Start Guide Overview](/matter/<docspace-docleaf-version>/matter-overview). The Matter over Thread demo requires an additional device to be used as the Hub's radio co-processor (RCP). You will therefore need some additional hardware and software.

## Radio Co-Processor Prerequisites

### Hardware

- 1x radio co-processor (RCP) compatible with RCP firmware images. Images are available for the following boards:

  - EFR32xG24: BRD2601, BRD2703, BRD4186, BRD4187
  - EFR32MG12: BRD4161, BRD4163, BRD4164, BRD4304, BRD4166 (TBS2), BRD4170, BRD4180

### Software

The Matter hub OpenThread RCP (ot-rcp) must be programmed with a bootloader and firmware image to act as the ot-rcp for the Raspberry Pi. You can obtain a copy of the latest version here: [Silicon Labs Matter Artifacts](/matter/<docspace-docleaf-version>/matter-prerequisites/matter-artifacts).

## A Typical Setup

A typical simple Matter over Thread network setup is shown in the following
image.

![Matter 15.4 Setup](./resources/thread-overview.png)

The setup consists of the following four elements:

1. A **Controller** such as an app running on a phone or the chip-tool running
    on a Linux box or Raspberry Pi.
2. An Open Thread Border Router (**OTBR**) running on a Linux box or Raspberry
    Pi.
3. A Radio Co-Processor (**RCP**), which the OTBR uses to communicate with the
    Thread network (not shown). This is attached to the Raspberry Pi.
4. An End Device such as a light or switch, which is the Matter Accessory
    Device (**MAD**).

The flow of the setup described above is as follows:

1. The controller commissions the End Device directly over Bluetooth – this
   makes the End Device join the Thread network and the Matter "Fabric".
2. After commissioning, the Bluetooth connection is terminated and all further
   communication is done over Matter.
3. The controller sends ZCL commands, such as the OnOff Toggle, and the End
   Device performs the corresponding action, such as turning the End Device's
   LED on or off

A Matter network can be built in a number of ways using a combination of Silicon
Labs hardware, a Raspberry Pi, and any external controller (MacBook, Ubuntu,
Android, etc.)

The suggested method, and the one illustrated in this quick-start guide, involves using a Raspberry Pi to function as both the
controller and the OTBR, with a Silicon Labs device as the MAD.

An alternate configuration is to use a MacBook as the controller, a Raspberry Pi
as the OTBR, and a Silicon Labs Device as the MAD. This requires additional
routing between the controller and OTBR.
