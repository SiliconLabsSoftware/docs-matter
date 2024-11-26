# Commands

Commmands are used to invoke a particular action. For instance an endpoint with the Doorlock client cluster can send an 'Invoke UnlockDoor' command to the Doorlock server to ask it to change the "LockState" attribute to unlocked. When validated and processed by the Doorlock server, this will then Unlock the door.

## Header File

This file contains the high level namespaces and constant definitions for Commands. In Simplicity Studio, this will be generated in the autogen/zap-generated/ folder of the matter project.

- [Commands](https://github.com/SiliconLabs/matter_extension/blob/main/third_party/matter_sdk/zzz_generated/app-common/app-common/zap-generated/ids/Commands.h)

The folder [```src/app```](https://github.com/SiliconLabs/matter_extension/tree/main/third_party/matter_sdk/src/app) contains several files related to the implementation of commands including interfaces, senders and handlers.
