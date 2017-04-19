# **Adcash Swift SDK 1.0**
Adcash Swift SDK is an advertising framework written in Swift 3!
- [Prerequisities](#prerequisities)
- [Third Party Dependencies](#third-party-dependencies)
- [Installation](#installation)
- [Banner](#banner)
- [Interstitial](#interstitial)
- [Rewarded Video](#rewarded-video)
- [Native](#native)
- [App Transport Security](#app-transport-security-ats)

## **Prerequisities**
* Zone ID(s) that you created at [Adcash website](https://www.adcash.com/)
* Xcode 8.1 or higher
* Swift 3.0 or higher
* Project deployment target 8.0 or higher

### **Third Party Dependencies**
Adcash Swift SDK uses [Alamofire 4.0](https://github.com/Alamofire/Alamofire) for networking operations. In order to use Adcash Swift SDK, you have to [add Alamofire](https://github.com/Alamofire/Alamofire#installation) into your project.

## **Installation**
### **CocoaPods**
[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

> CocoaPods 1.1.0+ is required.

To integrate Adcash Swift SDK and Alamofire into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '10.0'
use_frameworks!

target '<Your Target Name>' do
pod 'AdcashSwift', '1.0'
pod 'Alamofire', '~> 4.0'
end
```

Then, run the following command:

```bash
$ pod install
```

## **Manual**
1. Download the [Adcash Swift SDK](https://github.com/adcash/AdcashSwift/raw/master/AdcashSwift.framework.zip) and unzip it.
2. Right click on your project in the **Project Navigator** menu and select **Add Files to "name-of-your-project"**:
![Alt text](http://i2.wp.com/104.197.107.57/wp-content/uploads/2015/08/install-instructions-2.png)
3. Select the AdcashSwift.framework you just unzipped and press **Add**. Make sure you choose **Copy items if needed**.
![Alt text](http://i2.wp.com/104.197.107.57/wp-content/uploads/2015/08/install-instructions-3.png)
4. Follow [Alamofire Installation](https://github.com/Alamofire/Alamofire#installation) for adding it into your project.
5. **Build** and **Run**. Your project should start without any errors.
> Don't forget to add frameworks as 'Embedded Frameworks' in your targets 'General' settings

## Banner
1. Import the `AdcashSwift` module.
```swift
import AdcashSwift
```
2. **(Optional)** Set your view controller to conform the `AdcashBannerProtocol`.
```swift
class YourClass: UIViewController, AdcashBannerProtocol {
//...
}
```

3. Declare `AdcashBanner` variable in your class and initialize it.
```swift
//..
var banner: AdcashBanner!

banner = AdcashBanner(zoneID:"your-zone-id", viewController: self)
banner.translatesAutoresizingMaskIntoConstraints = false
self.view.addSubview(banner)
banner.delegate = self // You don't need this if you skipped step 2.

self.view.addConstraints(NSLayoutConstraint.constraints(withVisualFormat: "V:[banner(\(AdcashBannerSize))]|",
options: NSLayoutFormatOptions(rawValue: 0),
metrics: nil,
views: ["banner": banner!]
))
self.view.addConstraints(NSLayoutConstraint.constraints(withVisualFormat: "H:|[banner]|",
options: NSLayoutFormatOptions(rawValue: 0),
metrics: nil,
views: ["banner": banner!]
))
//..
```

4. Load the `AdcashBanner`.
```swift
banner.load()
```

5. **(Optional)** You can catch status updates from your ad by implementing the optional methods in `AdcashBannerProtocol`.
> If you skipped step 2, you don't have access to functions below.

```swift
func adReceived(banner: AdcashBanner)
func adFailedToReceive(banner: AdcashBanner, error: Error)
func adWillPresentScreen(banner: AdcashBanner)
func adWillDismissScreen(banner: AdcashBanner)
func adWillLeaveApplication(banner AdcashBanner)
```

## Interstitial
1. Import the `AdcashSwift` module.
```swift
import AdcashSwift
```

2. **(Optional)** Set your view controller to conform the `AdcashInterstitialProtocol`.
```swift
class YourClass: UIViewController, AdcashInterstitialProtocol {
//...
}
```

3. Declare `AdcashInterstitial` variable in your class and initialize it.
```swift
//..
var interstitial: AdcashInterstitial!

interstitial = AdcashInterstitial(zoneID:"your-zone-id")
interstitial.delegate = self // You don't need this if you skipped step 2.
//..
```

4. Load the `AdcashInterstitial`.
```swift
interstitial.load()
```
5. And present it to the screen.
```swift
interstitial.present(fromVC:self)
```
6. **(Optional)** You can catch status updates from your ad by implementing the optional methods in `AdcashInterstitialProtocol`.
> If you skipped step 2, you don't have access to functions below.

```swift
func adReceived(interstitial: AdcashInterstitial)
func adFailedToReceive(interstitial: AdcashInterstitial, error: Error)
func adWillPresentScreen(interstitial: AdcashInterstitial)
func adWillDismissScreen(interstitial: AdcashInterstitial)
func adWillLeaveApplication(interstitial: AdcashInterstitial)
```

## Rewarded Video
1. Import the `AdcashSwift` module.
```swift
import AdcashSwift
```

2. Set your view controller to conform the `AdcashRewardedVideoProtocol`.
```swift
class YourClass: UIViewController, AdcashRewardedVideoProtocol {
//...
}
```

3. Declare `AdcashRewardedVideo` variable in your class and initialize it.
```swift
//..
var rewarded: AdcashRewardedVideo!

rewarded = AdcashRewardedVideo(zoneID:"your-zone-id")
rewarded.delegate = self
//..
```

4. To play the `AdcashRewardedVideo`, call.
```swift
rewarded.playFrom(viewController:self)
```
5. You can catch status updates from your ad by implementing the optional methods in `AdcashRewardedVideoProtocol`.
> Be aware that `rewardedVideoDidComplete` is required to implement.
```swift
func adReceived(rewarded: AdcashRewardedVideo)
func adFailedToReceive(rewarded: AdcashRewardedVideo, error: Error)
func adWillPresentScreen(rewarded: AdcashRewardedVideo)
func adWillDismissScreen(rewarded: AdcashRewardedVideo)
func adWillLeaveApplication(rewarded: AdcashRewardedVideo)
func rewardedVideoDidComplete(rewarded: AdcashRewardedVideo, rewardName: String, rewardAmount: Int) //Required
```

## Native
1. Import the `AdcashSwift` module.
```swift
import AdcashSwift
```
2. **(Optional)** Set your view controller to conform `AdcashNativeProtocol`.
```swift
class YourClass: UIViewController, AdcashNativeProtocol {
//...
}
```
3. Declare `AdcashNative` variable in your class and initialize it:
```swift
var native: AdcashNative!

native = AdcashNative(zoneID:"your-zone-id")
native.delegate = self // You don't need this if you skipped step 2.
```
4. After loading, if response is successful, `AdcashNative` instance will be filled with information about the ad, such as:
+ Title               `func getAdTitle() -> String?`
+ Description         `func getAdDescription() -> String?`
+ Rating              `func getAdRating() -> String?`
+ Rating percentage   `func getAdRatingPercentage() -> String?`
+ Icon                `func getAdIconURL() -> URL?`
+ Image               `func getAdImageURL() -> URL?`
+ Action button text  `func getAdButtonText() -> String?`

to get these values, you should use corresponding functions above.

5. You can catch status updates from your ad by implementing the optional methods in `AdcashNativeProtocol`.
```swift
func adReceived(native: AdcashNative)
func adFailedToReceive(native: AdcashNative, error: Error)
```
6. You should also handle clicks and impressions so monetization won't get affected.
Call the function below when ad is visible on screen:
```swift
func trackImpression()
```
to handle clicks, call:
```swift
func openClick()
```

## App Transport Security (ATS)
With the release of iOS 9, Apple introduced a new default setting, called App Transport Security (ATS). ATS requires apps to make network connections only over SSL. It also allows specific encryption ciphers, SSL version and key length to be used when creating HTTPS connections.
Therefore, all iOS 9 devices running apps built with Xcode 7 that don’t disable ATS will be affected by this change. When a non-ATS compliant app attempts to serve an ad via HTTP on iOS 9, the following log message appears:

App Transport Security has blocked a cleartext HTTP (http://) resource load since it is insecure. Temporary exceptions can be configured via your app’s Info.plist file.

While Adcash acknowledges the need for secure connections, our ad network is not ready yet with the compliance of the requirements. Therefore, Adcash iOS SDK will work only by disabling App Transport Security in your `Info.plist`. You can do so by using one of the following two ways depending on your preference:
+ Disable ATS for all domains
This is the easiest solution. The only thing you need to do is to add the following configuration in your `Info.plist`.
```xml
<key>NSAppTransportSecurity</key>
<dict>
<key>NSAllowsArbitraryLoads</key>
<true/>
</dict>
```
It should look like this;
![Alt text](http://i1.wp.com/developer.adca.sh/wp-content/uploads/2015/10/app_transport_security_option1.png)

+ Disable ATS with some exceptions
You may only want ATS to work on domains you specifically know can support it. For example, if you may know that your server supports ATS and you would want things like login calls, and other requests to your server to use ATS, but ad requests to Adcash to bypass ATS requirements.
In this case you should set `NSAllowsArbitraryLoads` to true, then define the URLs that you want to be secure in your `NSExceptionDomains` dictionary. Each domain you wish to be secure should have its own dictionary, and the `NSExceptionAllowsInsecureHTTPLoads` for that dictionary should be set to false.
```xml
<key>NSAppTransportSecurity</key>
<dict>
<key>NSAllowsArbitraryLoads</key>
<true/>
<key>NSExceptionDomains</key>
<dict>
<key>secure.yourdomain.com</key>
<dict>
<key>NSExceptionAllowsInsecureHTTPLoads</key>
<false/>
</dict>
</dict>
</dict>
```
It should look like this;
![Alt text](http://i0.wp.com/developer.adca.sh/wp-content/uploads/2015/10/app_transport_security_option2.png)

## Support
If you need any help or assistance, you can contact us by sending email to mobile@adcash.com
