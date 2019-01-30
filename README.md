# Thingy Mesh Provisioning Demo v0.5
### Adaptation for EVK-NINA-B11x
This is a fork for thing52-mesh-provisioning-demo. It is meant to port the demo to EVK-NINA-B11x.

The LED is slightly different:
- Blink red several times: It's the OOB authentication, please type the number of blink to the app when asked.
- Turn on or off solid Blue: Thingy in normal operation, light is turn off or on. 

Use SW2 button as the Thing:52 button. It can be used to switch on and off the LED. The node can be reset powering off and on the EVK (or pressing the reset button) while pressing SW2.

### Overview
This is a quick guide on how to use the thingy52-mesh-provisioning-demo with the nRFMesh mobile app on iOS and Android.

There is a video demonstration of the demo here: https://www.youtube.com/watch?v=XthbU9NP0Yg

The demo can be used with as many Thingy as needed but it also works with just one Thingy. The Thingy firmware equiped with both Generic OnOff client and Generic OnOff Server.

The user can use nRF Mesh app to do provisioning for each Thingy. There is authentication required, please enter the number of LED blink you see on the Thingy when asked on the app. If you don't see any blink but it stops breathing Red type 0.

Inside each Thingy there are 2 elements, the first element has the foundation models and the Generic OnOff server, the second element has Generic OnOff client.

The user can choose to configure the node to be a light bulb by setting up the Generic OnOff server on the first element (binding app key and choose subscription address, for example group address 0xC001). Or can configure the node as light switch by configuring the Generic OnOff client (bind appkey and choose publication address, group 0xC001 for example)

One node can be light bulb or light switch or both at the same time. 

User can use mobile app to interact directly with the Generic OnOff server on the Thingy. It's the only model the app support direct control for now. 
(Any model will work with the app, but only for configuration, not direct control)

User can clear provisioning information of a node (reset the node) by holding the main button (on top of the thingy) and switch off and on the Thingy. Thingy will start as a fresh device

### Some color codes: 

- Breathing Red: Thingy is not provisioned and has not joined the network
- Breathing Green: Thingy is provisioned but has not been configured
- Blink white once: Thingy has been configured and has either a subscription/publication address. 
- Blink several times: It's the OOB authentication, please type the number of blink to the app when asked. 
- Turn on or off solid White: Thingy in normal operation, light is turn off or on. 

### Some information about the firmware
The firmware based on the proxy_server and proxy_client example in Mesh SDK v2.x. It uses some LED driver from Thingy SDK to control the LED.
The proprietary simple OnOff model was replaced with a simplified version of SIG Generic OnOff model so that it allows the mobile app to control the model from the app. 

- Thingy_provisioning_demo_generic_OnOff_BLINK: uses NRF_MESH_PROV_OOB_OUTPUT_ACTION_BLINK for OOB authentication, the Thingy blinks from 1 to 5 times when provisioning 


### Requirements
- Nordic nRF5x-DK or Segger J-Link debugger
- 2x5 1.27mm SWD cable
- Nordic Thingy:52 
- Nordic Thingy:52 SDK v2.1.0 with mod to work with SDK v15 logger module. It's provided as a .zip in this repo
- Nordic nRF5 SDK for Mesh v2.2.0
    - [https://www.nordicsemi.com/eng/Products/Bluetooth-low-energy/nRF5-SDK-for-Mesh](https://www.nordicsemi.com/eng/Products/Bluetooth-low-energy/nRF5-SDK-for-Mesh "nRF-Mesh-SDK")
- Nordic nRF5 SDK v15.0.0
- Segger Embedded Studio 

### Building the demo
To run the demo, you can use the precompiled firmware, or use Segger Embedded Studio to compile the firmware.

To compile the demo firmware and run the demo, please follow the steps:
1. Download and extract nRF5 Mesh SDK v2.2.0
2. Extract ThingySDKv2.1_mod.zip inside "external" in Mesh SDK. Should keep the "ThingySDKv2.1" folder name. 
3. Download and extract nRF5 SDK v15.0.0 
4. In SDK v15 \nRF5_SDK_15.0.0_a53641a\components\boards folder remove/rename file pca20020.h. It conflicts with the same file in Thingy SDK. 
5. Replace SDK v15 \nRF5_SDK_15.0.0_a53641a\components\boards\pca10040.h with the one in this repo.
6. Download and place the thingy_provisioning_demo_generic_OnOff folders in this repo into \examples\light_switch 
7. Connect the Thingy to the Debug port out on the DK or the Segger Jlink debugger. 
8. Do an erase all to remove the Thingy original firmware and bootloader
9. Open Segger Embedded Studio, and install the "nRF CPU Support Package". You can check it by click the main tool bar "Tools" -> "Package Manager", and search "nRF CPU Support Package".
10. Make sure you followed the SES.md guide in \doc\getting_started in nRF MESH SDK v2.2.0 of adding `SDK_ROOT` macro into SES, the same as when you started with Mesh examples (In Segger Embedded Studio, click "Tools" -> "Building", set the value for "Global Macros" to "SDK_ROOT=DIRECTORY_FOR_NORDIC_SDK15.0.0". 
11. Compile one of the project provided in this repo and flash the firmware, the softdevice is flashed automatically. 

### Known issues

 - Generic OnOff model in this demo was not merged with the Generic OnOff model in SDK v2.2.0
 





