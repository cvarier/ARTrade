# OANDA-ARTrade
A simple Android app created for the January 2018 OANDA hackathon. The app utilizes the ARCore SDK and detects flat surfaces as planes. It then lets you place a 3D object on a detected plane and interact with it.

## Inspiration
The original idea was to develop a mobile app that lets you interact with a static AR target and make a Forex trade. This app is an MVP which demonstrates how the original idea could be fully realized with some modifications. Currently it has the essentials to achieve this: 

1. A way to place a 3D object on a surface detected from a camera feed
2. Logic to detect that the object has been touched (the ARCore Java SDK does not include this functionality out of the box at the time of writing)
