# swiftExamples
Some personel solutions to general problems.
This solutions may not the best. They only include personel offers currently.

## Checking Service Error
Problem: While developing apps you connect enpoints almost everytime.So, you must check if any error like connection problems or non-authorized state, missing or wrong data structure etc. And checking these error types in every endpoint connection is really long, ugly and hard-to-maintenance.
Offer: Create a single class and only function to catch and display errors.

Error Detector Class Example : 


'''

public class BaseClass{
  func getErrorAlertIfAnyError(response : Alamofire.DataResponse<Any>, viewController : UIViewController? ) -> Bool {
        let errCode = (response.result.value as! NSDictionary).object(forKey: "ErrorCode") as? String
        if errCode != nil {
            let errMessage = (response.result.value as! NSDictionary).object(forKey: "ErrorMessage") as! String
            let alert = UIAlertController(title: "Hata", message: errMessage, preferredStyle: .alert)
            alert.addAction(UIAlertAction(title: "Tamam", style: .default, handler: nil))
            if viewController != nil {
                viewController?.present(alert, animated: true, completion: nil)
            }
            return true;
        }
        return false;
    }
}

'''
