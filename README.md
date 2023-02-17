# ROCO
The **RO**udanbout traffic **CO**nflict Dataset is a collection of traffic conflict events
 recorded at the two-lane roundabout at the intersection of State St. and W. Ellsworth Rd. in Ann Arbor, Michigan.
 Each event captures a 30-second duration of the conflict.
 The dataset provides the trajectories of the conflicts, 
 along with information about the reason, time, and effect of conflict.

- The data was collected from 9am to 7pm in the first week in September 2022.
- The data sample rate is 2.5Hz.
- MSight roadside perception system is used to extract the vehicle trajectories from raw video frames.

A related dataset: [RBTrajectoryData](https://github.com/michigan-traffic-lab/RBTrajectoryData)
provides the whole trajectory data in September 2022 at the same roundabout.
## Citation

## Sample Set
For this release, we are providing a sample set of 80 traffic conflict events.
These events were selected to provide a representative sample of the full dataset.
Each event is stored as a separate folder in the dataset.

## Data Format
### Data directory structure
The dataset is formatted into a zip file. The structure of the dataset is:
```
root/
    |- label.csv    # the label file of the dataset
    └- data/    # the raw trajectory data
        |- 2022-09-01_10-46-36-002396     # the trajectory data for one conflict event
        |   |- 2022-09-01 10-00-34-761973.json     # the trajectory file of one frame
        |   |- 2022-09-01 10-00-35-174299.json     # the trajectory file of one frame
        |   ...
        |- 2022-09-01_12-00-13-711073
        ...
```

### Label format
In the label CSV file, it contains the following fields:
- Severity: A level either 1 or 2 that indicates the severity of the traffic conflict
    - level 1 - a near-miss event
    - level 2 - a traffic accident
- Reason: A label that describes the reason for the traffic conflict.
    - 0 - entering a roundabout without yielding to the circulating vehicles
    - 0* - truck/bus/trailer entering a roundabout without yielding to the circulating vehicles
    - 1 - unnecessary stop in the circle
    - 2 - the truck/bus is too big and interferes with the traffic flow
    - 3 - improper lane use
    - 4 - secondary conflicts. The conflict is caused by previous events, like a previous conflict or previous crash
    - 5 - others
- IDs of the conflict vehicle pair, e.g. (23, 10). Notice: for secondary conflicts 
or for some conflicts that are hard to identify the conflict vehicles, denote ‘-1’.
 For the videos that have multiple conflicts,
 we only consider the pair of vehicles of the first (primary) conflict.
- The effect of the conflict on the traffic flow:
    - 0 - the traffic flow is not affected
    - 1 - one or two vehicles are forced to slow down in the circle due to the conflict
    - 2 - one or two vehicles are forced to stop in the circle due to the conflict
    - 3 - three or more vehicles are forced to slow down or stop in the circle due to the conflict
- The time offset (second) of the conflict event from the first frame (also the conflict name).
E.g., for a conflict named 

In the CSV file, the columns are:
```
event_timestamp,severity,reason,conflict trajectory pair,effect,time offset
```

### Trajectory format
The trajectory file is a JSON file that contains the trajectory of one frame.
Here is an example of the data in a json file
```
[
  {
    "id": "1",    # id of the vehicle (not universal unique id)
    "confidence": 0.849,    # confidence of the vehicle detection
    "lat": 42.301,    # the latitude coordinate of the vehicle position
    "lon": -83.698,   # the longitude coordinate of the vehicle position
    "uuid": "d3175b38-4e73-42f9-abb3-564b05788e90",       # the universal unique id of the vehicle
    "category": 0.0,      # the category of the vehicle (0: cars, 1: truck/bus/trailer)
    "speed": 1.536,      # the speed of the vehicle (m/s)
    "speed_heading": -1.741,      # the heading of the vehicle (north: 0, clock-wise)
    "predicted_future":     # predicted future vehicle position at the next six frames by our trajectory prediction model
      {
        "mean":     # the mean of the predicted future vehicle position
          [
            [42.22948273444069, -83.73878684072021], 
            [42.22951917166349, -83.73882189902272], 
            [42.22955463092418, -83.73885653671525], 
            [42.22959806281623, -83.73889505995245], 
            [42.229641211286584, -83.73891961750685], 
            [42.229683881407645, -83.73894786679861]
          ], 
        "std":     # the variance of the predicted future vehicle position
          [
            [0.0, 0.0], 
            [3.3877596180390264e-06, 5.4456512171775565e-06], 
            [3.7547065911662862e-06, 5.874294391702309e-06], 
            [4.419491663688003e-06, 6.963602536202044e-06], 
            [5.08341492670003e-06, 8.755623608381619e-06], 
            [6.052037926312747e-06, 1.0661085971328865e-05]
          ]
      }
  },
]
```

## Download
[roco_sample.zip](https://github.com/michigan-traffic-lab/ROCO/releases/download/v0.1/roco_sample.zip)

## Terms of Use
### Licenses
Unless specifically labeled otherwise, these Datasets are provided to You under a Creative Commons Attribution-Sharealike 4.0 International Public License (“CC BY-SA 4.0”) The CC BY-SA 4.0 may be accessed at https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode. When You download or use the Datasets from the Website or elsewhere, You are agreeing to comply with the terms of CC BY-SA 4.0 and also agreeing to the Dataset Terms. Where these Dataset Terms conflict with the terms of CC BY-SA 4.0, these Dataset Terms shall prevail.

## Acknowledgement
The dataset is supported by [Mcity](https://mcity.umich.edu/) and [National Science Foundation](https://www.nsf.gov/).

## Developers
Depu Meng - depum@umich.edu, Rusheng Zhang - rushengz@umich.edu, Shengyin Shen - shengyin@umich.edu

## Contact
Henry Liu - henryliu@umich.edu