### XCode Application Frameworks
* AutomateLockSDK.framework

### Installation
* Download the `AutomateLockSDK.framework` from Github
* Link the framework `AutomateLockSDK.framework` in your project. `Project target -> Frameworks, Libraries, and Embedded Content -> Embeded & Sign`
* Make sure `Info.plist` file includes `NSBluetoothAlwaysUsageDescription`, for example:
```xml
<key>NSBluetoothAlwaysUsageDescription</key>
<string>We need Bluetooth permission to scan and open Bluetooth locks.</string>
```
* Under `Build Phases > Embeded Frameworks`, click `"+"`, select `"Add Other..."` then navigate to `project root folder > AutomateLockSDK.framework > Frameworks` and select `CryptoSwift.framework`. Change the order of `Embeded Frameworks` to have `CryptoSwift.framework` above `AutomateLockSDK.framework`. Verify that `CryptoSwift.framework` is `Embeded & Sign` under `Frameworks, Libraries, and Embedded Content`
* For XCode 12.3 onwards:
- Under `Build Settings > Validate Workspace` change to `Yes`

### Setup

##### Import SDK in ViewController
`Import AutomateLockSDK`

##### Sample setup codes in ViewController

```swift
class ViewController: UIViewController {

    // Some codes...

    // declare instance of AutomateLockCtrl
    let automateLockCtrl = AutomateLockCtrl.sharedInstance;

    override func viewDidLoad() {
        super.viewDidLoad()

        // Some codes...

        // set delegate to be the current ViewController
        automateLockCtrl.delegate = self

        // initiate the SDK with your SDK key and return the status of initiation
        // you can't use other SDK methods until it has been initiated
        let initResult = automateLockCtrl.initialize(sdkKey: "[INSERT_YOUR_SDK_KEY_HERE]")

        // Some codes...
    }

    // scan and connect to the corresponding lock
    func connectLock(macAddress: String) {
        // return true after the lock connection request has been sent
        // return false if the SDK hasn't been initiated or SDK key is invalid
        let connectRequestResult = automateLockCtrl.connectLock(macAddress: macAddress)
    }

    // open lock using password
    func openLock(macAddress: String, password: String) {
        // return true after the lock open request has been sent
        // return false if the SDK hasn't been initiated or SDK key is invalid
        let openRequestResult = automateLockCtrl.connectLock(macAddress: macAddress, password: password)
    }

    // disconnect lock
    func disconnectLock(macAddress: String) {
        // return true after the lock has been disconnected (or if no lock is connected)
        // return false if the SDK hasn't been initiated or SDK key is invalid
        let disconnectResult = automateLockCtrl.connectLock(macAddress: macAddress)
    }

    // Some codes...
}

// implement delegate of AutomateLockSDK here
extension ViewController: AutomateLockCtrlDelegate {
    // trigger upon a lock successfully connected or fail
    func onConnect(macAddress: String, status: Bool) {
      // Some codes...
    }

    // trigger upon a lock successfully opened or fail
    func onOpen(macAddress: String, status: Bool) {
      // Some codes...
    }
}
```
