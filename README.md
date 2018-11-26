# Assist-MD-Public
This repo is only a README for employers.  The real repo is kept private for proprietary purposes and because private keys are shared amongst developers. 

# ASSIST-MD WEB APPLICATION

## Abstract

The world's technological ability to automate trivial task is growing at a stagering rate.  This is giving people the time and resources to perform higher level tasks that require human intelligence and creativity. The medical industry is a bit more difficult to automize since there are many more areas of liability. Unfortunately, a lot of a Doctor's time is spent on summarizing the events that took place during a surgery and if it is not, it is becasue the Doctor wrote the bear minimum or less.  This is a very specific area where the accuracy and comprehensiveness of Computer Vision could be utilized in such a way that would minimize doctors' time in the post-surgical procedure while optimizing the accuracely and thoroughness of the report.  

## Application Usage

As mentioned in the Abstract, Computer Vision will be utilized the the prototype for Assist-MD.  More specifically, we will employ the help of Joseph Redmon's YOLOv3 algorithm to start of with a set of weights that is well tuned to everyday objects and then shift the weights to gain a propensity for recognizing specific medical instruments based on the instrument's manufacturing serial number.  A compiled time series of the instruments used at each stage of the procedure will be reported on the ReactJS Web App, along with stats such as instruments used the most and the least, and the parts of the procedure that they were used for.  This information will be available for download on the front end web app as a PowerPoint presentation.

On of the biggest realizations made in the creation of this project was not to make inferences of instruments that the doctor is holding directly as there are many variables that could lead to the miscalculation of the inference such as camera angle and parts of the insturment not being visible.  Instead, we decided to make inferences of instruments that are on the table and not in use and then use a lambda funciton that will use the process of elimination based of an assumed knowledge of all the instruments opened from sterile bags in order to indirectly infer the instruments that the doctor is currently using.

For the prototype the video footage is captured through an app that can be viewed in the hvstream branch and sent to an S3 bucket.  From here, a Lambda function is triggered that takes that newly imported video frame and downloads it to an EC2 instance which then uses a darknet clone to infer the objects in the image.  After this process, the annotated image is then re-uploaded back to S3 and the front end web app queries this data in real time to keep up with new information.  Additionally, the web app has available a page for all historical videos that appear in the bucket with stats on each one, and a page for live video feed if a surgery is currently taking place.

## Steps to using Assist-MD Web App

- Simply go to the Website hosted on AWS S3 by clicking on the following link
  - [Assist-MD Website](http://assist-md-static-hosting.s3-website-us-west-2.amazonaws.com/)
### Alternatively, you can access the page locally by performing steps below
- Open terminal and perform the commands (for OSx):
  - `git clone git@github.com:brianhumphreys/Assist-MD.git`
  - `cd Assist-MD`
  - `npm i`
  - `export AWS_ACCESS_KEY=<key>`
  - `export AWS_SECRET_ACCESS_KEY=<key>`
  - `npm start`
