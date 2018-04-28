# ARTrade
A simple Android app created for the January 2018 OANDA hackathon. The app utilizes the ARCore SDK and detects flat surfaces as planes. It then lets you place a 3D object on a detected plane and interact with it.

## Inspiration
The original idea was to develop a mobile app that lets you interact with a static AR target and make a Forex trade. This app is an MVP which demonstrates how the original idea could be fully realized with some modifications. Currently it has the essentials to achieve this: 

1. A way to place a 3D object on a surface detected from a camera feed
2. Logic to detect that the object has been touched (the ARCore Java SDK does not include this functionality out of the box at the time of writing)

The following code snippet inside `ARActivity.java` is used to detect when an object has been tapped on the screen:

      Pose objectPose = mAnchors.get(0).getPose();
      Pose currentPose = hit.getHitPose();
      double distance = Math.sqrt(
              (currentPose.tx() - objectPose.tx()) * (currentPose.tx() - objectPose.tx()) +
                      (currentPose.ty() - objectPose.ty()) * (currentPose.ty() - objectPose.ty()) +
                          (currentPose.tz() - objectPose.tz()) * (currentPose.tz() - objectPose.tz())
      );

      if (distance < 0.1) {
          ...
      }

The above approach aims to calculate the distance between a point in space realized by a tap (stored in `currentPose`) and a point anchoring the 3D object (stored in `objectPose`) and decide if it is small enough to be considered within the boundaries of the actual object (the condition `distance < 0.1`, where units are in meters). This is a very crude approach, since it models the touchable area of the object as a sphere with a radius of 10 cm around the anchor point, but due to the limited object detection capabilities of the ARCore Android SDK, this is about the simplest way of realizing it without introducing external graphics libraries or writing a full-fledged raycaster.

**N.B.** The `Pose` object is modeled as a quaternion rotation followed by a translation vector, so to get the translation components, we use `tx()`, `ty()` and `tz()` instead of `qx()`, `qy()` and `qz()`.
