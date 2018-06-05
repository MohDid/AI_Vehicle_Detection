[//]: # (Image References)

[image1]: ./examples/videoInput.gif
[image2]: ./examples/Frames.PNG
[image3]: ./examples/Tiles.PNG




# Vehicle Detection using Linear SVM Classifier
The Project
---
Here, we are going to explain the steps to install/run the package and the main additions/modifications to the source package listed in credits.


#### Credits
##### This project is based on ajsmilutin's modification of the Udacity project https://github.com/ajsmilutin/CarND-Vehicle-Detection
---

## Package installation requirements
* Python 3.6.5
* OpenCV 3.4.1
* Scipy 1.1.0
* Numpy 1.14.3
* Other Libraries needed :
  - Scikit-learn 0.19.1 (Python library for machine learning)
  - Standardizing features by removing the mean and scaling to unit variance (using the class StandardScaler with its functions fit() and transform())
  - Splitting arrays or matrices into random train and test subsets (using the class model_selection with the splitter function train_test_split)
  - Implementing the Linear Support Vector Classification (instantiating the object with LinearSVC and using the functions fit(), predict() and score() )
* Matplotlib 2.2.2 (Python library for 2D plotting)
* Moviepy 0.2.3.4 (Python library for video editing)
* Scikit-image 0.13.1 (Python library for image processing)
  - Used for the Histogram of Oriented Gradients
  
#### This installation is done on Windows10 OS.
---
## How to run the project
Modifications were needed to use this project. We modified essentially the script car_finder.py and some modifications were made on the script lanefinder.py to not display the warning icon when the lane was lost.
The script car_finder.py was debugged because we found some errors on the window parameters for the heatmap. In car_finder.py, the casting of the Window variables into integers is necessary to avoid type incompatibility error while indexing the Heatmap matrix. There were some other errors due to incompatibilities of the libraries version which were not indicated in the source project. The project can now be used by downloading it and running car_finder.py.

----
## Creating a custom Dataset
Don't forget to install ffmpeg which is very useful for multimedia processing and also to be able to use the batch file for the tiles
Follow the instructions in this link : https://fr.wikihow.com/installer-FFmpeg-sur-Windows
The following script is used to create the tiles needed to feed the classifier.

First, you need to install ImageMagick from their website : http://www.imagemagick.org/script/download.php.

You can choose the release depending on your operating system. We used the release ImageMagick-7.0.7-36-Q16-x64-dll.exe.

When magick is installed, you can run the following script that is going to take your input video (don’t forget to change it with the name of your video). The video will be seperated in frames that will be stored in the folder /frames. Finally, the frames will be cut in 64x64 tiles that will be stored in the folder /tiles.
```bash
mkdir frames
ffmpeg -i input_Video.mp4 -f image2 frames/frame-%03d.png
mkdir tiles
for file in frames/*.png; 
  do magick convert -crop 64x64 +repage $file tiles/`basename $file .png`-tile%02d.png; 
  done
```

#### This step is very important because, you need it for the creation of your own dataset.

---
### Sorting the tiles
Next, you will need to sort your tiles folder and to separate them in two classes and store them in two different folders that you can call myNewVehicle and myNewNonVehicle. This step must be done meticulously because it can have a negative impact on the performances of your SVM.

| Video Input | Frames  | Tiles |
|-------------|---------|-------|
|![][image1]| ![][image2] | ![][image3]|

There are some videos showing the effects of a wrongly trained SVM based on some inadequate samples that we put in the dump folder. Check the dataset NewVehicles.rar in the folder /wrong_dataset and the video cars_test3_wrongly_trained.mp4 in the folder /Used_Videos.

Finally, you need to sort out white tiles from your folders because it crashes the script when we run train_svm.py


---
## Training the classifier
After doing all the previous steps, you can train your SVM by running train_svm.py. Finally, you can run car_finder.py to generate your output videos. Don’t forget to create a folder to store them in it and you can modify its path in the script car_finder.py as well as the video files that you would like to process.
#### Car_finder.py
```python
    video_files = ['myInput.mp4']
    output_path = "output_videos"
```
