# Explanation: detectScene(image: CIImage)
#### iOS III challenge to try and explain the detectScene functionality in Machine Learning Vision


1. For starers, the function is called within the imagePicker's ```didFinishPickingMediaWithInfo``` function. It begins when the user has selected an image to be set as the image for the ```imageView```. The selected image is converted to a CIImage and set into the detectScene function.
      ```Swift
        guard let ciImage = CIImage(image: pickedImage) else {
                     displayString(string: "Unable to convert image to CIImage.");
                     return
                 }

                 detectScene(image: ciImage)
      ```
2. The first few things that happen within detectScene are mostly for the user to understand that the call was successful and is working. On line 90, we see  the textView is set to "detecting scene" via the displayString method.    

      Next, the ML model that is being used (in the case of this example, it is VGG16) is set to a variable simply called ```model```. The setting of this variable is managed by guard/try statements and provides the user an error statement should the setting fail. 
      
3. Using the ```model``` variable we just set, we create a vision request via ```VNCoreMLRequest```, and assign the output of this request to a variable called ```results```   
      
      When the request gets finished, the results will be looped through via a for-loop, and are printed out 
      ```Swift                
      for result in results {
            self?.displayString(string: "\(Int(result.confidence * 100))% \(result.identifier)")
      } 
      ```
      
      However, the request has not be utilized, at this point in the code, and will need to be used within a ```VNImageRequestHandler```
      
4. We create this ```VNImageRequestHandler``` and assign it to a variable called ```handler```, as seen beginning on line 125. We use the ```perform``` method to execute the request   
      ```Swift
      try handler.perform([request])
      ```
      and begin the actual detection of the scene, thus, will attempt to execute the for-loop and output that we see on the screen when the application is running. The ``` perform``` method is protected via a do/catch block, with appropriate error descriptions provided for the user.   
      
---
#### Additional Notes
An activity indicator is created on 19 and is simply called `activity indicator`.   
```Swift
@IBOutlet weak var activityIndicator: UIActivityIndicatorView!
```
The activity indictor is displayed on screen in the form of a spinning loading-type circle. It is accessed multiple times within `detectScene` to either `startAnimating()` or `stopAnimating()`, as it pretains to the execution of the request and loading of the results.

    
      
      
 
   
