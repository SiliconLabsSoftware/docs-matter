# Loading firmware Expansion board

Loading firmware on Expansion board can be done using Teraterm or kermit


1. Make sure that the switches on the expansion board are towards UART side.
![Switch Position before firmware flash](images/si917-board.png)

2. For updating the SiWx917 Firmware, refer [Updating the RS9116 Firmware](https://docs.silabs.com/rs9116/wiseconnect/2.0/update-evk-firmware). Instructions are the same for both SiWx917 and RS9116.
3. Once that is done make sure to make switches back to Expansion mode, while using it with the host platform.
![Switch Position after firmware flash](images/mg21-si917-board.jpg)