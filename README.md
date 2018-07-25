# Watson Visual Recognition Lunch and Learn (Galvanize - 08.25.18)

## Presentation
[Watson Visual Recognition Service](assets/ibm-watson-visual-api.pdf)

## IBM Cloud Sign up for this event only
[IBM Cloud](https://ibm.biz/vr072518)

## Additional Links
1. [Watson Visual Recognition Service Home](https://www.ibm.com/watson/services/visual-recognition/)
2. [Tutorials and Documentation](https://console.bluemix.net/docs/services/visual-recognition/getting-started.html)
3. [API for different SDKs](https://www.ibm.com/watson/developercloud/visual-recognition/api/v3/curl.html?curl)
4. [API Explorer ](https://watson-api-explorer.ng.bluemix.net/apis/visual-recognition-v3)
5. [IBM Data Studio](https://dataplatform.cloud.ibm.com/home?context=analytics)
6. [IBM Cloud Dashboard](https://console.bluemix.net/dashboard/apps/)

## CURL commands for lunch and learn

### Built in models
1. Set environment variable for test images

    `export watson_visual_directory="/Users/<username>/Desktop/galvanize-07.24.18/gsk-hackathon-images/test"`

    `export watson_visual_directory_root="/Users/<username>/Desktop/galvanize-07.24.18"`

2. Set environment variable for the visual service secret key. You can get this from the `credentials` tab in the visual recognition service on IBM cloud dashboard after your have created the visual recognition resource.

    `export watson_visual_key=<secret_key>`

3. Classify an image using URL

    https://github.com/lidderupk/watson-visual-galvanize-08.25.18/blob/master/assets/sf-cable-car.jpg

    `curl -u "apikey:$watson_visual_key" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?url=https://github.com/lidderupk/watson-visual-galvanize-08.25.18/blob/master/assets/sf-cable-car.jpg?raw=true&version=2018-03-19"`


4. Single local image

    `curl -X POST -u "apikey:$watson_visual_key" -F "images_file=@$watson_visual_directory_root/kids.jpeg" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"`

5. Multiple local images - zip file

    `zip multiple_images.zip dog.png kids.jpeg`

    `curl -X POST -u "apikey:$watson_visual_key" -F "images_file=@$watson_visual_directory_root/multiple_images.zip" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"`


6. Face model

    `curl -X POST -u "apikey:$watson_visual_key" -F "images_file=@$watson_visual_directory_root/kids.jpeg" -F "threshold=0.6" "https://gateway.watsonplatform.net/visual-recognition/api/v3/detect_faces?version=2018-03-19"`

7. Food model
    `curl -X POST -u "apikey:$watson_visual_key" -F "images_file=@$watson_visual_directory_root/fruitbowl.jpeg" -F "classifier_ids=food" -F "threshold=0.6" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"`
￼

### Custom models
8. Get all classifiers

    `curl -u "apikey:$watson_visual_key" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classifiers?verbose=true&version=2018-03-19"`

9. Use the default model

    `curl -X POST -u "apikey:$watson_visual_key" -F "images_file=@$watson_visual_directory/mucinex-1.JPG" -F "threshold=0.6" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"`

10. Use both default and the custom models

    `curl -X POST -u "apikey:$watson_visual_key" -F "images_file=@$watson_visual_directory/mucinex-1.JPG" -F "classifier_ids=MedicinexModel_257596841,default" -F "threshold=0" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"`
