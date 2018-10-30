# Real-Time Learning Tracker


The *Real-Time Learning Tracker* is an interactive learning widget that can be intergrated in a learner dashboard destined for MOOC learners on the  edX  platform.  This **real-time** feedback mechanism for edX learners consists of three different feedback complexity versions and each one of them uses low-level data from trace logs and converts it into behavioural indicators that describe several learning habits of the learners. By means of a bar chart appearing in a pop-up window at the bottom right of every MOOC page, it provides learners with real-time feedback on their learning behaviour comparing it to previously successful learners. 

The Complex version of the *Real-Time Learning Tracker* is presented in action via this screencast: https://www.youtube.com/watch?v=jlhfIt9iCAE&t=53s

## Functional Architecture

The working architecture of the *Real-Time Learning Tracker* has three components as shown in the figure below.

![alt text](https://github.com/gatou92/RealTimeLearningTracker/blob/master/images/RLT_FuncionalArchitecture.jpg)
 
1. **edX component (Javascript)**
	- contains the code responsible for real-time logging learners’ activity during the course.
	- contains the calculation of the metric values of each active learner in the course from 	the logged activity data 
	- loads each version (complex-intermediate-simple) of the *Real-Time Learning Tracker* on the edX pages in a pop-up window, based on learner’s edX id.

2. **Server backend (Javascript)**
	- developed with the [node.js](https://nodejs.org/en/) server environment, the back-end is 
	the part of the *Real-Time Learning Tracker* responsible for managing requests.
	- new events traced from the **real-time logger** code are logged to [MongoDB](https://www.mongodb.com) database and all the  necessary logs for the learners’ metric computation as well as the **Average** and the **Most Engaged Graduate** profiles are sent back to the client.
3. **Local component (Python)**
	- the successful learner profiles (**Average** and **Most Engaged Graduate**) are generated by calculating the metric values from low-level activity data form a previous edition of the course and are inserted into the MongoDB database.


## Metrics available

The metrics are calculated considering data generated from the first day of the course.

1. Number of video lecture watched
2. Number of quiz questions submitted
3. Amount of time spent on the course pages (in minutes)
4. Amount of time spent watching video lectures (in minutes)
5. The ratio of time spent watching video lectures while on the course pages (%)
6. The amount of forum contributions (#threads/#responses/#comments created) on the course pages
7. The ratio of learners' Engagement (%) - aggregated activity during the course computed based on all six aforementioned behavioural indicators

