---
layout: project
title:  "Improving Webgazer"
pseudo-path: "/projects/improving-webgazer"
given-date:  "Dec, 2017"
categories: improving-webgazer deep-learning computer-vision brown-university coursework
tag: "improving-webgazer"
tags: improving-webgazer deep-learning computer-vision brown-university coursework
languages: "Python, Javascript"
project-github:  "https://github.com/eecatlin/webgazer"
private-github:  false
project-page:  true
project-page:  "/assets/csci-1430-final-report.pdf"
menu-img:  "/assets/improving-webgazer.png"
menu-img-alt: "Improving Webgazer"
brown: true
---
In this project Emma Caitlin, Shannon Ward, Benjamin Ward, and I attempted to improve [Webazer][webgazer], an online real time eye tracking software for Brown's [CSCI 1430: Computer Vision][compvis]. We tried to improve [Webgazer][webgazer]'s real time performance by altering its Javascript. Additionally I wrote a convolutional neural net to show that the implementation of one could drastically improve the accuracy of [Webgazer][webgazer] without sacrificing much speed. We were unable to gain much of an increase in accuracy through any of the Javascript changes, but the results of the the convolutional neural net supported our original hypothesis.

You can view our work by following the link to the github. Navigate to [webgazer/WebGazer-master/src/][src] to see our work. The file [gazerCNN.py][CNN] contains the main code for the convolutional neural net I wrote. Other files and directories related to the convolutional neural net are [wipeCNNResults.py][wipe], [CNNModels][models], and [CNNResults][results].

You can read our final report by following the link to the project's independant page. At first glance it may seem similar to a research paper, but it is somewhat oddly formatted to better serve the goals of the course's final project.

[webgazer]: https://webgazer.cs.brown.edu/
[compvis]: http://cs.brown.edu/courses/csci1430/
[src]: https://github.com/eecatlin/webgazer/tree/master/WebGazer-master/src
[CNN]: https://github.com/eecatlin/webgazer/blob/master/WebGazer-master/src/gazerCNN.py
[wipe]: https://github.com/eecatlin/webgazer/blob/master/WebGazer-master/src/wipeCNNResults.py
[models]: https://github.com/eecatlin/webgazer/tree/master/WebGazer-master/src/CNNmodels
[results]: https://github.com/eecatlin/webgazer/tree/master/WebGazer-master/src/CNNresults