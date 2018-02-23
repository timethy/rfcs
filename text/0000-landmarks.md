# Feature Name

## Summary
[summary]: #summary

Adding user-identified Landmarks into the SLAM Pose Graph optimization problem.
Landmarks (e.g. 2D-Codes, Images, SURF-features) identified and tracked by the user are used to optimize both the relative position between consecutive nodes and additional loop-closure by observing the same landmark from nodes of the same submap or consecutive submaps respectively.
Its an open questions into what use-cases should/can be covered (see #discussion)

## Motivation
[motivation]: #motivation

The main motivation is to fuse landmark observations from visual SLAM approaches (QR-tags, SURF features) with the LIDAR-based SLAM approach currently used in Cartographer.

The result should be improved loop-closure performance, 

## Approach
[approach]: #approach

The user supplies matched landmark data, in the form of a set of landmarks that are observed at a specific time.
Multiple sources of landmark inputs (e.g. one per camera) is possible.
The user can also supply weights

The landmarks are then stored in a datastructure that makes evaluating the landmark observation at given times (the time of the node) efficiently possible for all landmark id.



## Discussion Points
[discussion]: #discussion

### Use-cases covered

I (@timethy) thinks that its relatively easy to cover:
1. Tracking uniquely identifiable (fixed) Landmarks of which the relative pose can be measured in 6 DoF (e. g. by a camera and tags of known size).
2. Tracking of features over the multiple stereo-frames (i.e. SURF features extracted and matched in a stereo-frame and consecutive stereo frames).

A little more difficult but I think 
1. Beacons, e.g. landmarks of which only the range (or even simply only proximity) can be measured,
2. Tags with a non-fixed size (only 5 DoF)
3. Tags with bearing-only measurement (i.e. SURF features captured by a monocular camera set-up),
would also be a common use-case worth considering.

Another point where I would be happy to get some input as to how-to implement it, is the integration of Landmarks in the local SLAM problem.
It seems to me that for consecutive nodes with intersecting sets of landmarks measurements could get another factor to be used (i.e. odometry, laser and landmark) cost terms.



