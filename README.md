# Clear-Reset-All-Views-on-Logout-to-prevent-getting-dump-data-from-previous-logged-in-user
Use this code to clear data of all view objects on logout to prevent dump data of previous logged in user even if you logged in from new user or other account. 


### Put this code in Logout method to Clear all data on logout after clearing shared class and userdefualts use the code below.

```swift
                            if(status == 1)
                            {
                                DispatchQueue.main.async {
                                    ReusableClass.sharedInstance.hideActivityIndicator()
                    
                                    LoginUserInfo.sharedInstance.removeUserInfo()
                                    userdefault.removeObject(forKey: "SelectedClass")
                                    userdefault.removeObject(forKey: "SelectedSection")
                                    userdefault.removeObject(forKey: MaindataKey)
                                    userdefault.set(false, forKey: "LoginCheck")
                   
                                    //Below are the codes to clean data on Logout
                                    
                                    let toViewController = mainStoryboard.instantiateViewController(withIdentifier: "KSLoginViewController") as! KSLoginViewController// Login view controller here
                                    let fromView = UIApplication.shared.keyWindow!.rootViewController!.view
                                    UIApplication.shared.keyWindow?.rootViewController = toViewController
                                    
                                    let toView = toViewController.view
                                    toView?.addSubview(fromView!)
                                    
                                    UIView.animate(withDuration: 0.38, delay: 0.2, options: [], animations: {
                                        fromView?.transform = CGAffineTransform(translationX: -UIScreen.main.bounds.width, y: 0)
                                    }, completion: { finished in
                                        fromView?.removeFromSuperview()
                                    })
                                    
                                }

```


### If Your PushViewcontroller navigation not working on login screen then put this code in status 1 reponse after saving the reponse data .

```swift

                                if(status == 1)
                                {
                                    DispatchQueue.main.async {
                                        ReusableClass.sharedInstance.hideActivityIndicator()
                                        
                                        //Save your reponse data to shread class or userdefaults here
                                        //.....
                                        userdefault.set(true, forKey: "LoginCheck")
                                        
                                        
                                        // Method to implement naviagtion controller to work pusviewcontroller on login screen
                                        
                                        let teacher = studentStoryboard.instantiateViewController(withIdentifier: "KSStudentDashboardVC") as! KSStudentDashboardVC
                                        let aObjNavi = UINavigationController(rootViewController: teacher)
                                        let appDelegate: AppDelegate = (UIApplication.shared.delegate as? AppDelegate)!
                                        appDelegate.window?.rootViewController = aObjNavi
  
                                      
                                    }
                                    }

```
