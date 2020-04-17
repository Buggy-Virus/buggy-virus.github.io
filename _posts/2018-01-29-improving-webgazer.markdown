---
layout: post
title:  "Improving Webgazer"
date:   2018-01-29 02:00:00 -0000
categories: improving-webgazer deep-learning computer-vision brown-university coursework
tags: improving-webgazer deep-learning computer-vision brown-university coursework
---

I recently added the project [Improving Webgazer][improving] to my [projects page][projects], a project I completed in a team for Brown University’s course [CSCI 1430: Computer Vision][vis]. The intent of the project was to improve [Webgazer][webgazer] which is a browser based eye tracking service. After opening the application and providing it with training data as to where you are looking at your screen, it will continuously provide an estimate as to which point of the screen you are looking at based on the image from your webcam.

The way it accomplishes this is by first identifying the position of your eyes using a common facial recognition model, then using machine learning on a rectangle containing both your eyes to build a model based on the training data you provide by watching your mouse as you move it around the screen.

There are various ways one can go about improving webgazer. The goal of our project was to improve the accuracy of Webgazer as the application ran in real time, or, using a data set of images of various individuals’ faces, create an alternative machine learning method with greater accuracy.

Accuracy was based upon an estimate’s mean squared error from [Tobii eye tracker][better] estimate, another more refined eye tracking application.

$$D(x, y) = \sqrt{(x+y)^2}$$

<center><span style="font-size:14px;color:#828282;text-align:center;"> Block 1: Mean squared error.</span></center>

&nbsp;

My team tried to improve Webgazer’s real time application through various methods, such as altering parameters or the data fed into the machine learning process. My contribution was showing that a convolutional neural net based on Anjith George and Aurobinda Routray’s paper, [Real-time Eye Gaze Direction Classification Using Convolutional Neural Network][paper], would outperform Webgazer in terms of accuracy while being able to maintain a reasonable frames per second.

<center><img src="/assets/improving-webgazer/architecture.png" alt="Architecture" style="width:627px;height:220px;text-align:center;"></center>

<center><span style="font-size:14px;color:#828282;text-align:center;"> Figure 1: CNN architecture. </span></center>

&nbsp;


The architecture of the CNN consisted of 9 layers, one input layer, three convolutional layers of size 7x7 then 5x5 then 3x3, each followed by a 2x2 max pooling layers, a fully connected layer of 4096, then a final fully  connected layer with 1 unit. A 42x50 pixel images of both eyes were fed through the CNN twice, giving four estimates, one for each eye in the $$x$$ and $$y$$ axes. Averaging the results from each eye together, we got our final estimate.

 The results of my CNN had 40% less error than Webgazer, while still being able to maintaining a speed of processing 51 frames per second for each of the four estimates. This showed that a CNN could replace the current machine learning method of Webgazer while still maintaining a tolerable frames per second in real time.

If you want to look further into the details of this project, check out my group’s [final report][pap]. It goes in depth on my contributions as well as my teammates. It is structured loosely like a research paper, but is slightly more bloated in order to fulfill the assignment’s criteria.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

[improving]: /projects/improving-webgazer
[projects]: /projects/
[vis]: http://cs.brown.edu/courses/csci1430/
[webgazer]: https://webgazer.cs.brown.edu/
[better]: https://tobiigaming.com/
[paper]: https://arxiv.org/abs/1605.05258
[pap]: /assets/csci-1430-final-report.pdf



