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

Follow few steps for simple and fast SmartBeacon-SDK use:
For the below example we want to notify user when he will exit the region determined by SmartBeacon private proximity UUID.
The following code shows implementation in a basic View Controller named DemoViewController.

DemoViewController.h

// generated code by Xcode
#import <UIKit/UIKit.h>

@interface DemoViewController : UIViewController
@end

DemoViewController.m

#import "DemoViewController.h"

// make sure you add frameworks header
#import <CoreLocation/CoreLocation.h>
#import <SmartBeacon-SDK/SmartBeacon.h>

@interface DemoViewController () <SBLocationManagerDelegate>
@end

@implementation DemoViewController

// UIViewController life cycle

- (void)loadView
{
    [super loadView];
  
    // load UI
}

- (void)viewDidLoad
{
    [super viewDidLoad];

    // getting shared instance
    SBInstanceSingleton *sbInstance = [SBInstanceSingleton sharedInstance];
    
    // add entire SmartBeacon region 
    [sbInstance addEntireBeaconRegionWithIdentifier:@"my_identifier"];
    
    // or specifically one or more SmartBeacon region by specifying major and minor id (minor is optional)
    // [sbInstance addBeaconRegionWithMajor:1234 withIdentifier:@"my_identifier_1234"];
    // [sbInstance addBeaconRegionWithMajor:5678 withMinor:9012 withIdentifier:@"my_identifier_xyz"];
    
    // note:
    // - identifiers must be unique for each beacon region
    // - use addEntireBeaconRegionWithIdentifier: once
    // or addBeaconRegionWithMajor:withIdentifier:, addBeaconRegionWithMajor:withMinor:withIdentifier as many times as you need it
    
    // start listening beacon region
    [sbIntance startServicesForTarget:self];
}

// SBLocationManagerDelegate

// This method is called when the user exit the listened region.
// It is not immediate, we can wait over 10 seconds before call.
- (void)beaconManager:(SBLocationManager *)manager didExitRegion:(CLRegion *)region
{
    // Local notifications are visible only if the app is in background (and if the user allowed them).
    //
    // That's why, in this case, we open an UIAlertView popup if app is visible and a local notification if is in background.

    if (UIApplicationStateActive == [[UIApplication sharedApplication] applicationState])
    {
        UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:@"SmartBeaconSDK" message:@"Bye, see you next time !" delegate:nil cancelButtonTitle:@"Close" otherButtonTitles:nil];
        [alertView show];
    }
    else if (UIApplicationStateBackground == [[UIApplication sharedApplication] applicationState])
    {
        UILocalNotification *localNotification = [[UILocalNotification alloc] init];
        [localNotification setSoundName:UILocalNotificationDefaultSoundName];
        [localNotification setAlertBody:@"SmartBeaconSDK - Bye, see you next time !"];
        
        [[UIApplication sharedApplication] presentLocalNotificationNow:localNotification];
    }
}

// let see SBLocationManagerDelegate protocol for more useful methods

@end




