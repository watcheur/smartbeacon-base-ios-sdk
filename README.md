SmartBeacon Base iOS SDK for iOS 7
====================

Introduction
--------------------


Overview
--------------------


Installation
--------------------

Follow steps described below to install SmartBeaconSDK library:

1. Download SmartBeacon-SDK.framework and copy it into your project directory.

2. Open your Xcode project, go to targets pane, then go to Build Phases tab. In Link Binary With Libraries section, click +. In the popup window click add other at the bottom and select SmartBeacon-SDK.framework file.

SmartBeacon-SDK requires following native iOS framework:
* CoreLocation.framework

3. Congrats! Yes you did it!


Integration
--------------------

Follow few steps for simple SmartBeacon-SDK use:
For the below example we want to notify user when he will exit the region determined by SmartBeacon private proximity UUID.
The following code shows implementation in a basic View Controller.

