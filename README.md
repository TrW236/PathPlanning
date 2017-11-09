# Path Planning

## Usage and Dependencies

* Please visit the [repository](https://github.com/udacity/CarND-Path-Planning-Project) from Udacity.

* Replace all the files in `src` folder.

* The file `spline.h` can be found on this [website](http://kluge.in-chemnitz.de/opensource/spline/).

## Result

The video is uploaded on Youtube. [link](https://www.youtube.com/watch?v=7R0xwKGxPU0&index=5&list=PLNDTbGbATLcED0iX8K-zY3vrNbwhxV8gC)

## Model Description

I used four states in the path planner:

1. In the state `MAX VELOCITY` the vehicle tries to drive with the maximal velocity straightforward. 
    * When our car detected that the forgoing car is too close to us, the state will be changed to `FOLLOW CAR`.

2. In the state `FOLLOW CAR` the vehicle follows the forgoing car with the velocity of the followed car. 
    * When our car detected that the forgoing car is not too close to us any more, the state will be changed to `MAX VELOCITY`. 
    * When our car detected that the following velocity (is the same as that of the forgoing car) is less than 45 mph, the state will be changed to `PREPARE LANE CHANGING`.

3. In the state `PREPARE LANE CHANGING` the vehicle follows the forgoing car and check, whether there are other cars, which can block the lane changing of our car, on the left and right side. 
    * Our car will first check the left side and then check the right side. 
    * When the forgoing car is not too close any more, the state will be changed back to `MAX VELOCITY`. 
    * When our car checked that there are no cars on the left or right side, the state will be changed to `LANE CHANGING`. 

4. In the state `LANE CHANGING` our vehicle is changing the lane.
    * When our car has finished the lane changing, the state will be changed back to `MAX VELOCITY`.

```
   <Start>
      |
      |
      v
[MAX VELOCITY] <-------------------------> [FOLLOW CAR]
    ^    ^                                      |
    |    |                                      |
    |    |                                      |
    |    |------------------------------        |
    |                                  |        |
    |                                  |        v
[LANE CHANGING] <------------------ [PREPARE LANE CHANGING]

```   

## References

1. Udacity Self-Driving Car Engineer Nanodegree

2. [Spline interpolation](http://kluge.in-chemnitz.de/opensource/spline/)