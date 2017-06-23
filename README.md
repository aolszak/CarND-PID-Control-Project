# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

## Video
https://vimeo.com/222894299

## Reflections

####1. PID components effect.

As we know from the course P component stands for proportional relation between steering and CTE - it result oscilating movement around reference drive track and overshooting. D stands for differential relation and it helps overcoming oscilating movement and overshooting - drive track smoothly converges with the reference. I stands for integral relation and it helps overcome problem of systematic bias, so the car adjusts the steering over time if there is no improvement of position over time.

In practice I've found that those components have different effect on the driving style a specially when they are used together. I've found that 'P' component is affecting momentary sensitivity of the car, reaction latency and how close to the center of the track car stays. 'I' component was affecting initial drive smoothness and turning on bigger curves. 'D' component was affecting how often can was adjusting it position and how big were single adjustments.

####2. Hyperparameters tuning.

My first step was to randomly choose a parameter set which could let the car drive through the track with speed 20mph. After having initial working point for tuning I've started to analyse what effect have every PID component. After tuning good results for 20mph I've increased the speed to 30mph and started tuning again on higher speed. I've made the same for 40mph and did some checks with speed up to 90mph - with 70mph the controller was still able to handle correct driving, but it was looking a bit unsafe.

I decided to stay with speed 40mph and those parameters:

* P = 0.12
* I = 0.0015
* D = 2.0