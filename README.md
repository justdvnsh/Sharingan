# c0de_BrEaKeRs - Sharingan !

### Sharingan - A complete optical monitoring ecosystem !
![img](/desktop-software/sharingan.png)

Sharingan is an optical monitoring tool for programmers. Basically it is an ecosystem to maintain a good eye health for programmers or anyone who wishes to use it. The ecosystem is divided into two parts :-

1) __Desktop Software__ : This desktop software is an eye health tracking tool which has three main features.
    
    - __Blink-Detection__ : ![img](/images/blink.png)
        - __Idea__ :
            Since , we know that Technology is a rapidly growing field , thus we need to keep ourselves updated to everything in order to survive this highly competitve field. But in keeping up-to-date to the field, we often neglect the health of our eyes. We often forget to blink , and as we all know , that blinking is one of the most important feature of our eyes as it keeps the eye lubricated and helps us prevent from various types of diseases, Hence , This feature keeps a track on the eye of a user and informs them about the number of times they have blinked. The data will be updated on the website for you to have a measure . 
        
        - __How__ :
            We know that we can extract specific facial structures by knowing the indexes of the particular face parts. In terms of blink detection, we are only interested in two sets of facial structures — the eyes.
            Each eye is represented by 6 (x, y)-coordinates, starting at the left-corner of the eye (as if you were looking at the person), and then working clockwise around the remainder of the region
            ![img](https://www.pyimagesearch.com/wp-content/uploads/2017/04/blink_detection_6_landmarks.jpg)Based on this image, we should take away on key point:
            There is a relation between the width and the height of these coordinates.
            Based on the work by Soukupová and Čech in their 2016 paper, Real-Time Eye Blink Detection using Facial Landmarks, we can then derive an equation that reflects this relation called the eye aspect ratio (EAR): ![img](https://www.pyimagesearch.com/wp-content/uploads/2017/04/blink_detection_equation.png)
            Where p1, …, p6 are 2D facial landmark locations.
            The numerator of this equation computes the distance between the vertical eye landmarks while the denominator computes the distance between horizontal eye landmarks, weighting the denominator appropriately since there is only one set of horizontal points but two sets of vertical points. we’ll find out, the eye aspect ratio is approximately constant while the eye is open, but will rapidly fall to zero when a blink is taking place.
            Using this simple equation, we can avoid image processing techniques and simply rely on the ratio of eye landmark distances to determine if a person is blinking.
        
        - __Future Improvements__ :
            This in terms of features is a basic tool because eye-blink detection in itself is a great feature to have. Now , We can have this system to help __aid the paralysed__. Since the paralysed can only move their eyes and blink, this feature can be of great use for them, as we can make a great paralysed assisting tool, based on their number of blinks.

            Talking about number of blinks , we can also have this as a software, where a user can pre-define a certain number of blinks to perform a certain task.

2) __Drowsiness_Detection__ : ![img](/images/drowsiness_detection.png)

    - __Idea__ : 
            We all know that programming is all about problem-solving and many times this problem-solving attitude becomes an addiction for many of us. Thus in order to feed our addiction we spend days and nights coding and solving various problems. And we know that coding is a tiring task if done well, this leads to many of us sleeping on the spot or with the laptop on. Thus , our drowsiness detection feature helps the programmers in informing that they are falling asleep and they should most probably find a better spot to sleep and shut down the system to save some electricity.

    - __How__ :
            We know about the EAR or Eye-Aspect-Ratio from above. This feature can be thought of as an extention to the above feature . Basically we are keeping a track of the EAR .  If the eye aspect ratio falls below this threshold, we’ll start counting the number of frames the person has closed their eyes for. And thus if the number of frames the person has closed their eyes in exceeds , we'll sound an alarm.

    - __Future Improvements__ :
            This feature can be very well brought into the drowsiness or sleep detection for the drivers. We know that accidents are common now and almost 60-70% of accidents happen due to unattentiveness of the driver or because he/she felt asleep. Using this feature , we can easily track the driver and maybe stop the vehicle if the driver falls asleep.

3) __Posture Detection__: ![img](/images/posture_detection.png)

    - __Idea__ : 
            We do not need to know this that our posture is responsible for many things. From maintaing a proper balance in the body or keeping our bones in proper shape , to making us look more confident. But a programmers job is most of the time not a good posture appreciator. Most of the times we have our posture slouched towards the screen. Thus , we implemented this feature into Sharnigan to help programmers maintain a good posture. However, I may remind you that this feature is still in its __beta phase__. It may contain bugs.

    - __How__ :
            In order to determine the distance from our camera to a known object or marker, we are going to utilize triangle similarity.

            The triangle similarity goes something like this: Let’s say we have a marker or object with a known width W. We then place this marker some distance D from our camera. We take a picture of our object using our camera and then measure the apparent width in pixels P. This allows us to derive the perceived focal length F of our camera:

            F = (P x  D) / W

            As I continue to move my camera both closer and farther away from the object/marker, I can apply the triangle similarity to determine the distance of the object to the camera:

            D’ = (W x F) / P

    - __Future Improvements__ :
            This feature is still in its beta phase , but still is quite powerful. It is measuring the distance to the object. Future improvements of the feature can be enourmous. We can have a self adjusting chair based on this feature or maybe an ample of robots to measure the distance based on the camera, as processed images give way better results than normal vectors.

            This feature can also be used up with a CNN to develop a simple working model of a real-world self-driving car.

__The Website__ :
    ![img](/images/website.png)
    The website is basically a community of healthy hackers, who can share healthy posts , see their stats , follow and unfollow a user and have a chat with them.

---

### Rooms For Improvements !

1) First and foremost , we could see that due to noise in a video stream, subpar facial landmark detections, or fast changes in viewing angle, a simple threshold on the eye aspect ratio could produce a false-positive detection, reporting that a blink had taken place when in reality the person had not blinked.

To make our blink detector more robust to these challenges, Soukupová and Čech recommend:

Computing the eye aspect ratio for the N-th frame, along with the eye aspect ratios for N – 6 and N + 6 frames, then concatenating these eye aspect ratios to form a 13 dimensional feature vector.
Training a Support Vector Machine (SVM) on these feature vectors.
Soukupová and Čech report that the combination of the temporal-based feature vector and SVM classifier helps reduce false-positive blink detections and improves the overall accuracy of the blink detector.

2) Since we are processing the opencv images into a pyQt window, we need to use the video frame as a separate image passed into the window per .01 milisecond. This forces the distance_detection algorithm to detect_distance every 1/100th milisecond, and thus not giving accurate and particular results to maintain a certain threshold, to detect the slouchiness of the user.

3) Since a timer is already running per .01th of a milisecond , it is getting extremely hard to run a new instance of the timer class , simultaneously to peform time related processing.

---

### Tools and Tech Stack !

1) PyQt5 was solely used to create the GUI of the program ( The Desktop software )

2) OpenCv was used to process images and frames.

3) Flask was used to make the web server.

4) Sqlite was used as the database.

5) Bootstrap was used as a frontend framework.

---

### How to run !

1) __Software__

Run these commands first to install the PyQt5 Software and OpenCv
```sh
pip install PyQt5
pip install PyQt5-tools
pip install openCv
```

Then navigate to desktop-software dir and run ```python gui.py```

2) __Website __

First install all the dependencies of the project mentioned in requirements.txt

run these commands to populate the database.
```sh
flask db init
flask db migrate -m 'users table'
flask db upgrade
flask db migrate -m 'posts table'
flask db upgrade
```

Finally run ```flask run``` and navigate to ```localhost:5000```

---

### License

This project is MIT licensed. 
This project uses an image of the Sharingan which could be subject to copyright !

---
