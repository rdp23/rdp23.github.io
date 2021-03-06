## A GENTLE INTRODUCTION TO MOTION ESTIMATION USING OPTICAL FLOW  
Computer vision has come a long way since its advent in the past century. With increase in
processing power and research in this field in leaps and bounds, we have been able to
accomplish impressive feats.  

Computer Vision involves dealing with both static and dynamic scenes. This post aims to provide
a gentle introduction to dealing with moving objects and moving scenes.  

It is always prudent to start a topic with some motivation. So let's see if some potential areas of
application can pique your interest.
 - Surely you must have recorded lots of videos from your phone's camera. More likely than
not, the quality would have suffered due to an unsteady hand. Motion estimation
techniques can come to your rescue in stabilizing the video. Video compression softwares
too exploit these techniques.
 - This is the era of drones. Using computer vision and motion estimation algorithms, the
drones could very well detect and identify moving targets and act accordingly.
 - There's another application of motion estimation. However, with this one, you might end up
owing your life to it: Accident Prediction. The idea is that some computer vision software
would process real-time footage from, say, a dashcam and estimate the velocity and
proximity of the nearby vehicles. This could potentially allow a driver to act on the
predictions and steer away from a collision course!

### Motion Representation in 2d  

An image is a projection of a 3d setting onto a 2d frame. So when the 3d setting or parts of it
move, naturally, its projection onto the 2d frame would also have an element of motion in it.  

The image can be stored in any colorspace. RGB, Grayscale and HSV are some of them. While
we can work with any of them, we will restrict ourselves to images in grayscale in this discussion,
as it is easy to work with. Also most of the information desired about the image can be obtained
from this representation.  

In grayscale representation, each pixel in a frame has an 'intensity' (trivially, brightness) value. 0
represents the black color and 255 represents white.

If our scene is dynamic, the part of the scene that corresponds to one set of pixels in the frame,
would then correspond to some other set of pixels in the *next* frame.
So the pattern of intensities of pixels in a location in previous frame would now appear on another
location of the next frame.
It is as if the pixels themselves were translating across the frame!
So our first step towards estimating the motion of the objects in the real world, would be to track
the 'pixels' corresponding to our objects of interest across the frames.

### The Optical Flow Equation  
So far we have established that at the pixel level, motion of an object can be represented by the
translation of points or pixels constituting that object to a different position in subsequent frames.
Now to get a measure of how ‘fast’ and in ‘which direction’ a particular pixels is moving, we need
to quantify things and introduce equations. Enter Optical Flow!   
The Optical Flow equation
basically summarizes the motion of individual pixels in terms of gradients of intensity in the image
sequence at a particular point. So what do we obtain upon solving the optical flow equation? We
get the velocity vector( the horizontal and the vertical components) of the pixel at that instant of
time. Without further ado, let us go about thinking how one might arrive at such an equation
