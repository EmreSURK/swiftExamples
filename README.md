# swiftExamples
Some personel solutions to general problems.
This solutions may not the best. They only include personel offers to solve some problems.

## Detecting Service Error
**Problem:** While developing apps you connect endpoints almost everytime.So, you must check if any error like connection problems or non-authorized state, missing or wrong data structure etc. And checking these error types in every endpoint connection is really long, ugly and hard-to-maintenance.

**Offer:** Create a single class and only function to catch and display errors.

Error Detector Class Example : 

```swift
public class BaseClass{
  func getErrorAlertIfAnyError(response : Alamofire.DataResponse<Any>, viewController : UIViewController? ) -> Bool {
        let errCode = (response.result.value as! NSDictionary).object(forKey: "ErrorCode") as? String
        if errCode != nil {
            let errMessage = (response.result.value as! NSDictionary).object(forKey: "ErrorMessage") as! String
            let alert = UIAlertController(title: "Error", message: errMessage, preferredStyle: .alert)
            alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
            if viewController != nil {
                viewController?.present(alert, animated: true, completion: nil)
            }
            return true;
        }
        return false;
    }
}

```

**This is how to use it with Alomofire;**

if ErrorCode is not nil this will return **true** and **show** an alert that shows ErrorMessage

```swift
let error = BaseClass().getErrorAlertIfAnyError(response: response, viewController: self)
```

if ErrorCode is not nil this will return **true** and **but won't show** an alert that shows ErrorMessage

```swift
let error = BaseClass().getErrorAlertIfAnyError(response: response, viewController: nil)
```

You can use `return` to avoid running code below.

```swift
let error = BaseClass().getErrorAlertIfAnyError(response: response, viewController: self)
if error { return; }
```

